```mermaid
flowchart TD
    %% Début de l'interaction avec le sous-traitant
    START([Ticket Pret pour Assignation]) --> SELECT[Selectionner Sous-traitant Optimal]
    
    %% Phase de sélection
    SELECT --> CHECK_EXPERTISE{Expertise\nRequise?}
    CHECK_EXPERTISE -->|Messagerie| FILTER_MAIL[Filtrer Experts Messagerie]
    CHECK_EXPERTISE -->|Reseau| FILTER_NET[Filtrer Experts Reseau]
    CHECK_EXPERTISE -->|Securite| FILTER_SEC[Filtrer Experts Securite]
    CHECK_EXPERTISE -->|Materiel| FILTER_HW[Filtrer Experts Materiel]
    
    FILTER_MAIL --> CHECK_AVAILABILITY
    FILTER_NET --> CHECK_AVAILABILITY
    FILTER_SEC --> CHECK_AVAILABILITY
    FILTER_HW --> CHECK_AVAILABILITY
    
    %% Vérification disponibilité
    CHECK_AVAILABILITY[Verifier Disponibilite] --> AVAILABILITY{Charge\nInferieure 80%?}
    AVAILABILITY -->|Non| NEXT_CONTRACTOR[Candidat Suivant]
    NEXT_CONTRACTOR --> CHECK_AVAILABILITY
    AVAILABILITY -->|Oui| CHECK_SLA[Verifier SLA Compatible]
    
    %% Validation SLA
    CHECK_SLA --> SLA_OK{SLA\nCompatible?}
    SLA_OK -->|Non| NEXT_CONTRACTOR
    SLA_OK -->|Oui| VALIDATE_CHOICE[Valider Choix Final]
    
    %% Préparation de l'assignation
    VALIDATE_CHOICE --> PREP_ASSIGNMENT[Preparer Dossier Assignation]
    PREP_ASSIGNMENT --> LOAD_TEMPLATE[Charger Template Email]
    LOAD_TEMPLATE --> FILL_DATA[Remplir Donnees Ticket]
    
    %% Données incluses dans l'email
    FILL_DATA --> INCLUDE_PROBLEM[Inclure Description Probleme]
    INCLUDE_PROBLEM --> INCLUDE_PRIORITY[Inclure Priorite et SLA]
    INCLUDE_PRIORITY --> INCLUDE_CONTACTS[Inclure Contacts Utilisateurs]
    INCLUDE_CONTACTS --> INCLUDE_FILES[Joindre Fichiers Diagnostic]
    INCLUDE_FILES --> REVIEW_EMAIL[Relire Email Assignation]
    
    %% Envoi et traçabilité
    REVIEW_EMAIL --> SEND_ASSIGNMENT[Envoyer Email Assignation]
    SEND_ASSIGNMENT --> LOG_SENT[Enregistrer Communication Envoyee]
    LOG_SENT --> UPDATE_STATUS[Mettre a jour Statut ASSIGNED]
    UPDATE_STATUS --> START_SLA_TIMER[Demarrer Compteur SLA]
    
    %% Monitoring automatique en parallèle
    START_SLA_TIMER --> MONITOR_LOOP{Surveillance\nSLA Active}
    
    %% Branche monitoring SLA
    MONITOR_LOOP --> CHECK_ACK_TIME[Verifier Delai Accuse]
    CHECK_ACK_TIME --> ACK_DELAY{Accuse en\nRetard?}
    ACK_DELAY -->|Non| CHECK_RESPONSE_TIME
    ACK_DELAY -->|Oui| SEND_ACK_REMINDER[Envoyer Rappel Accuse]
    SEND_ACK_REMINDER --> LOG_REMINDER[Enregistrer Relance]
    LOG_REMINDER --> CHECK_RESPONSE_TIME
    
    CHECK_RESPONSE_TIME[Verifier Delai Reponse] --> RESP_DELAY{Reponse en\nRetard?}
    RESP_DELAY -->|Non| CHECK_RESOLUTION_TIME
    RESP_DELAY -->|Oui| SEND_RESP_REMINDER[Envoyer Rappel Reponse]
    SEND_RESP_REMINDER --> LOG_RESP_REMINDER[Enregistrer Relance Reponse]
    LOG_RESP_REMINDER --> CHECK_RESOLUTION_TIME
    
    CHECK_RESOLUTION_TIME[Verifier Delai Resolution] --> RESOL_DELAY{Resolution en\nRetard?}
    RESOL_DELAY -->|Non| WAIT_COMMUNICATION
    RESOL_DELAY -->|Oui| ESCALATE_DELAY[Escalader Retard]
    
    %% Escalade en cas de retard critique
    ESCALATE_DELAY --> CRITICAL_DELAY{Retard\nCritique?}
    CRITICAL_DELAY -->|Non| SEND_FIRM_REMINDER[Envoyer Relance Ferme]
    CRITICAL_DELAY -->|Oui| ESCALATE_MANAGER[Contacter Manager Sous-traitant]
    SEND_FIRM_REMINDER --> WAIT_COMMUNICATION
    ESCALATE_MANAGER --> PENALIZE{Appliquer\nPenalites?}
    PENALIZE -->|Oui| APPLY_PENALTY[Appliquer Penalite Contractuelle]
    PENALIZE -->|Non| FINAL_WARNING[Dernier Avertissement]
    APPLY_PENALTY --> CONSIDER_CHANGE
    FINAL_WARNING --> CONSIDER_CHANGE
    
    CONSIDER_CHANGE[Considerer Changement] --> CHANGE_CONTRACTOR{Changer\nSous-traitant?}
    CHANGE_CONTRACTOR -->|Oui| TERMINATE_CONTRACT[Resilier Assignation]
    CHANGE_CONTRACTOR -->|Non| WAIT_COMMUNICATION
    TERMINATE_CONTRACT --> SELECT
    
    %% Branche réception communications
    WAIT_COMMUNICATION[Attendre Communication] --> RECEIVE_COMM[Recevoir Communication]
    RECEIVE_COMM --> COMM_TYPE{Type de\nCommunication?}
    
    %% Types de communication
    COMM_TYPE -->|Accuse Reception| PROCESS_ACK[Traiter Accuse Reception]
    COMM_TYPE -->|Demande Info| PROCESS_REQUEST[Traiter Demande Info]
    COMM_TYPE -->|Rapport Avancement| PROCESS_PROGRESS[Traiter Rapport Avancement]
    COMM_TYPE -->|Livraison Solution| PROCESS_DELIVERY[Traiter Livraison]
    COMM_TYPE -->|Probleme Bloquant| PROCESS_ISSUE[Traiter Probleme]
    
    %% Traitement accusé de réception
    PROCESS_ACK --> LOG_ACK[Enregistrer Accuse]
    LOG_ACK --> UPDATE_ACK_STATUS[Statut ASSIGNED vers ACKNOWLEDGED]
    UPDATE_ACK_STATUS --> STOP_ACK_TIMER[Arreter Timer Accuse]
    STOP_ACK_TIMER --> WAIT_COMMUNICATION
    
    %% Traitement demande d'informations
    PROCESS_REQUEST --> ANALYZE_REQUEST[Analyser Demande]
    ANALYZE_REQUEST --> INFO_AVAILABLE{Informations\nDisponibles?}
    INFO_AVAILABLE -->|Oui| PROVIDE_INFO[Fournir Informations]
    INFO_AVAILABLE -->|Non| GATHER_INFO[Collecter Informations Manquantes]
    GATHER_INFO --> CONTACT_USERS[Contacter Utilisateurs]
    CONTACT_USERS --> PROVIDE_INFO
    PROVIDE_INFO --> SEND_INFO_RESPONSE[Envoyer Reponse Info]
    SEND_INFO_RESPONSE --> LOG_INFO_SENT[Enregistrer Envoi Info]
    LOG_INFO_SENT --> WAIT_COMMUNICATION
    
    %% Traitement rapport d'avancement
    PROCESS_PROGRESS --> LOG_PROGRESS[Enregistrer Avancement]
    LOG_PROGRESS --> UPDATE_PROGRESS[Mettre a jour Pourcentage]
    UPDATE_PROGRESS --> PROGRESS_SATISFACTORY{Avancement\nSatisfaisant?}
    PROGRESS_SATISFACTORY -->|Oui| ACKNOWLEDGE_PROGRESS[Accuser Reception Avancement]
    PROGRESS_SATISFACTORY -->|Non| REQUEST_CLARIFICATION[Demander Precisions]
    ACKNOWLEDGE_PROGRESS --> WAIT_COMMUNICATION
    REQUEST_CLARIFICATION --> SEND_CLARIF_REQUEST[Envoyer Demande Precisions]
    SEND_CLARIF_REQUEST --> LOG_CLARIF[Enregistrer Demande Precisions]
    LOG_CLARIF --> WAIT_COMMUNICATION
    
    %% Traitement problème bloquant
    PROCESS_ISSUE --> ANALYZE_ISSUE[Analyser Probleme Bloquant]
    ANALYZE_ISSUE --> ISSUE_TYPE{Type de\nProbleme?}
    ISSUE_TYPE -->|Acces Systeme| PROVIDE_ACCESS[Fournir Acces]
    ISSUE_TYPE -->|Information Technique| PROVIDE_TECH_INFO[Fournir Info Technique]
    ISSUE_TYPE -->|Autorisation| PROVIDE_AUTHORIZATION[Donner Autorisation]
    ISSUE_TYPE -->|Materiel| PROVIDE_HARDWARE[Fournir Materiel]
    
    PROVIDE_ACCESS --> ISSUE_RESOLVED
    PROVIDE_TECH_INFO --> ISSUE_RESOLVED
    PROVIDE_AUTHORIZATION --> ISSUE_RESOLVED
    PROVIDE_HARDWARE --> ISSUE_RESOLVED
    
    ISSUE_RESOLVED[Probleme Resolu] --> NOTIFY_RESOLUTION[Notifier Resolution]
    NOTIFY_RESOLUTION --> LOG_ISSUE_RESOLUTION[Enregistrer Resolution Probleme]
    LOG_ISSUE_RESOLUTION --> WAIT_COMMUNICATION
    
    %% Traitement livraison solution
    PROCESS_DELIVERY --> RECEIVE_DELIVERABLES[Recevoir Livrables]
    RECEIVE_DELIVERABLES --> CHECK_COMPLETENESS[Verifier Completude]
    CHECK_COMPLETENESS --> COMPLETE{Livraison\nComplete?}
    COMPLETE -->|Non| REQUEST_MISSING[Demander Elements Manquants]
    REQUEST_MISSING --> WAIT_COMMUNICATION
    COMPLETE -->|Oui| START_VALIDATION[Demarrer Validation]
    
    %% Phase de validation
    START_VALIDATION --> TECHNICAL_TEST[Tests Techniques]
    TECHNICAL_TEST --> TECH_OK{Tests Tech\nPasses?}
    TECH_OK -->|Non| REJECT_TECHNICAL[Rejeter pour Defaut Technique]
    TECH_OK -->|Oui| USER_ACCEPTANCE_TEST[Tests Utilisateurs]
    
    REJECT_TECHNICAL --> DOCUMENT_ISSUES[Documenter Problemes]
    DOCUMENT_ISSUES --> REQUEST_FIX[Demander Correction]
    REQUEST_FIX --> WAIT_COMMUNICATION
    
    USER_ACCEPTANCE_TEST --> USER_OK{Tests Users\nPasses?}
    USER_OK -->|Non| REJECT_FUNCTIONAL[Rejeter pour Defaut Fonctionnel]
    USER_OK -->|Oui| ACCEPT_DELIVERY[Accepter Livraison]
    
    REJECT_FUNCTIONAL --> DOCUMENT_FUNC_ISSUES[Documenter Defauts Fonctionnels]
    DOCUMENT_FUNC_ISSUES --> REQUEST_FUNC_FIX[Demander Correction Fonctionnelle]
    REQUEST_FUNC_FIX --> WAIT_COMMUNICATION
    
    %% Acceptation finale et évaluation
    ACCEPT_DELIVERY --> UPDATE_RESOLVED[Statut vers RESOLVED]
    UPDATE_RESOLVED --> STOP_SLA_TIMER[Arreter Compteur SLA]
    STOP_SLA_TIMER --> CALCULATE_METRICS[Calculer Metriques Performance]
    
    CALCULATE_METRICS --> EVAL_RESPONSE_TIME[Evaluer Temps Reponse]
    EVAL_RESPONSE_TIME --> EVAL_RESOLUTION_TIME[Evaluer Temps Resolution]
    EVAL_RESOLUTION_TIME --> EVAL_COMMUNICATION[Evaluer Qualite Communication]
    EVAL_COMMUNICATION --> EVAL_SOLUTION_QUALITY[Evaluer Qualite Solution]
    
    %% Scoring final
    EVAL_SOLUTION_QUALITY --> CALCULATE_SCORE[Calculer Score Global]
    CALCULATE_SCORE --> SCORE_RANGE{Score\nGlobal?}
    SCORE_RANGE -->|Excellent 90-100| RATE_5_STARS[Noter 5 etoiles]
    SCORE_RANGE -->|Bon 75-89| RATE_4_STARS[Noter 4 etoiles]
    SCORE_RANGE -->|Moyen 60-74| RATE_3_STARS[Noter 3 etoiles]
    SCORE_RANGE -->|Faible 40-59| RATE_2_STARS[Noter 2 etoiles]
    SCORE_RANGE -->|Mauvais 0-39| RATE_1_STAR[Noter 1 etoile]
    
    RATE_5_STARS --> UPDATE_CONTRACTOR_RATING
    RATE_4_STARS --> UPDATE_CONTRACTOR_RATING
    RATE_3_STARS --> UPDATE_CONTRACTOR_RATING
    RATE_2_STARS --> UPDATE_CONTRACTOR_RATING
    RATE_1_STAR --> UPDATE_CONTRACTOR_RATING
    
    UPDATE_CONTRACTOR_RATING[Mettre a jour Rating Sous-traitant] --> SAVE_FEEDBACK[Sauvegarder Commentaires]
    SAVE_FEEDBACK --> CLOSE_INTERACTION[Clore Interaction]
    CLOSE_INTERACTION --> END([Interaction Terminee])
    
    %% Retour vers monitoring si pas terminé
    MONITOR_LOOP --> WAIT_COMMUNICATION
    
    %% Styles pour différents types d'activités
    classDef startEnd fill:#e1f5fe,stroke:#01579b,stroke-width:3px
    classDef selection fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef communication fill:#e8f5e8,stroke:#1b5e20,stroke-width:2px
    classDef monitoring fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef validation fill:#fff8e1,stroke:#f57f17,stroke-width:2px
    classDef escalation fill:#ffebee,stroke:#b71c1c,stroke-width:3px
    classDef evaluation fill:#f1f8e9,stroke:#33691e,stroke-width:2px
    classDef decision fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    
    %% Application des styles
    class START,END startEnd
    class SELECT,FILTER_MAIL,FILTER_NET,FILTER_SEC,FILTER_HW,CHECK_AVAILABILITY,VALIDATE_CHOICE selection
    class SEND_ASSIGNMENT,RECEIVE_COMM,PROVIDE_INFO,SEND_INFO_RESPONSE,NOTIFY_RESOLUTION communication
    class MONITOR_LOOP,CHECK_ACK_TIME,CHECK_RESPONSE_TIME,CHECK_RESOLUTION_TIME,START_SLA_TIMER monitoring
    class TECHNICAL_TEST,USER_ACCEPTANCE_TEST,START_VALIDATION,ACCEPT_DELIVERY validation
    class ESCALATE_DELAY,ESCALATE_MANAGER,APPLY_PENALTY,TERMINATE_CONTRACT escalation
    class CALCULATE_METRICS,EVAL_RESPONSE_TIME,CALCULATE_SCORE,UPDATE_CONTRACTOR_RATING evaluation
    class CHECK_EXPERTISE,AVAILABILITY,SLA_OK,ACK_DELAY,RESP_DELAY,CHANGE_CONTRACTOR,COMPLETE,TECH_OK,USER_OK decision
    ```