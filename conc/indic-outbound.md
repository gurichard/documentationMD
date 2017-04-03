Indicateurs CCCP
===============
### Indicateurs agents
#### Etat de la leg cible
##### user_vocal_state
- indicateur existant
- valeur possible
  - outbound (nouveau)
  - agent_invited (nouveau)
  - agent_trying (nouveau)
  - agent_ringing (nouveau)
  - agent_connected (nouveau)
  - remote_invite (nouveau)
  - remote_trying (nouveau)
  - remote_ringing (nouveau)
  - remote_connected (nouveau)
  - outbound_hold (nouveau)
  - available (existant, inbound)
  - invite (existant, inbound)
  - trying (existant, inbound)
  - ringing (existant, inbound)
  - contact (existant, inbound)
  - hold (existant, inbound)
  - postprocessing (existant, wrapup)
  - nom de pause (existant, withdrawal)
  - ...
- indicateurs utilisés de la librairie applicative:
  - last_state_name
  - busy_count
  - last_state_display_name
  - outbound_state (nouveau)
  - outbound_hold_flag.value (nouveau)


#### Date du début de l'appel sortant en cours (leg remote)
##### vocal_user_current_task_start_date
- indicateur existant
- valeur = une date isoformat
- indicateurs utilisés de la librairie applicative:
  - tasks.last.task.start_date
  - tasks.last.task.end_date
  - last_outbound_call_start.value (nouveau)

#### Nombre de legs cibles tentées pour la journée en cours
##### Indicateur
###### user_total_leg_count
- nouvel indicateur
- valeur par défault = 0
- est la somme de tout les total_leg_count sur 24h depuis les sessions

#### Nombre de legs cibles contactées pour la journée en cours
##### Indicateur
###### user_contacted_leg_count
- nouvel indicateur
- valeur par défault = 0
- est la somme de tout les contacted_leg_count sur 24h depuis les sessions

#### Nombre de legs cibles en échec pour la journée en cours
##### Indicateur
###### user_failed_leg_count
- nouvel indicateur - non demandé
- valeur par défault = 0
- est la somme de tout les failed_leg_count sur 24h depuis les sessions

#### Nombre de legs cibles annulées pour la journée en cours
##### Indicateur
###### user_canceled_leg_count
- nouvel indicateur - non demandé
- valeur par défault = 0
- est la somme de tout les canceled_leg_count sur 24h depuis les sessions

#### Durée totale en contact pour la journée en cours
##### Indicateur
###### user_outbound_contact_total_duration
- nouvel indicateur
- indicateurs utilisés de la librairie applicative:
  - outbound_contact_duration.value
  - sessions.last.session.profile_name (pour acceder à l'ensemble des sessions sur la journée)
  - login

#### Durée maximale en contact pour la journée en cours
##### Indicateur
###### user_outbound_contact_maximum_duration
- nouvel indicateur
- indicateurs utilisés de la librairie applicative:
  - outbound_contact_duration.value
  - sessions.last.session.profile_name (pour acceder à l'ensemble des sessions sur la journée)
  - login

#### Durée moyenne en contact pour la journée en cours
##### Indicateur
###### user_outbound_contact_average_duration
- nouvel indicateur
- indicateurs utilisés de la librairie applicative:
  - outbound_contact_duration.value
  - contacted_leg_count.value
  - sessions.last.session.profile_name (pour acceder à l'ensemble des sessions sur la journée)
  - login

### Indicateurs communication
Ici les indicateurs pour les communications entrantes ont été surchargé.
Seul ceux ci sont actifs:
- communication_create_date
- from
- to
- channel (indicateur par défault, sans subscribe)
- total_duration (chrono start invite)
- managing_duration (chrono start contact)

#### Type de communication
##### communicaion_type
- indicateur par défault, sans subscribe
- valeur par défault: inbound
- si communication sortant, valeur = outbound

Indicateurs librairie applicative
=================================
### Indicateurs agents
#### Leg agent ouverte
##### Indicateur
###### outbound_state (value=str)
- disconnected: par défault ou suite à connection.disconnected (normal et sortant).
- agent_invite: suite à un progressing.invite si le state est outbound.
- agent_trying: lors d'un trying sur la leg agent.
- agent_ringing: lors d'un ringing sur la leg agent ou un trying code 183.
- agent_connected: suite à connection.connected sur leg agent, à la fin de la leg remote, et outbound_cancel.

#### Etat de la leg cible
##### Indicateurs
###### outbound_state (value=str)
- disconnected: par défault ou suite à connection.disconnected (normal et sortant).
- agent_invite: suite à un progressing.invite si le state est outbound et sur la leg agent.
- agent_trying: lors d'un trying sur la leg agent.
- agent_ringing: lors d'un ringing sur la leg agent ou un trying code 183.
- agent_connected: suite à connection.connected sur la leg agent, à la fin de la leg remote, outbound_cancel et connection failed.
- remote_invite: suite à un progressing.invite si le state est outbound et sur la leg remote.
- remote_trying: lors d'un trying sur la leg remote.
- remote_ringing: lors d'un ringing sur la leg remote ou un trying code 183.
- remote_connected: suite à connection.connected sur la leg remote.

###### outbound_hold_flag (value=bool)
- valeur par défault : false
- suite à un connection.disconnected (agent ou remote) : false
- suite à un user.contact : false
- suite à un user.hold : true

#### Date/heure du début d'appel sortant en cours
##### Indicateur
###### outbound_call_start_time (value=str)
- valeur par défault = stop
- suite à un progressing.invite si le state est outbound et sur la leg remote = iso_now()
- suite à outbound_cancel = stop
- suite à un connection.disconnected (normal et sortant) = stop
- suite à un connection.failed = stop

#### Nombre de legs cibles tentées pour la session en cours
##### Indicateur
###### total_leg_count
- valeur par défault = '0'
- incrémentation lors d'un remote_invite

#### Nombre de legs cibles contactées pour la session en cours
##### Indicateur
###### contacted_leg_count
- valeur par défault = '0'
- incrémentation lors d'un remote_connected.

#### Nombre de legs cibles en échec pour la session en cours
##### Indicateur
###### failed_leg_count
- valeur par défault = '0'
- incrémentation lors d'un connection.failed.

#### Nombre de legs cibles annulées pour la session en cours
##### Indicateur
###### canceled_leg_count
- valeur par défault = '0'
- incrémentation lors d'un outbound_cancel

#### Durée en état sortant cumulée pour la journée en cours
##### Indicateur
###### state_group_outbound.duration('0')
- Indicateur natif

#### Durée en contact sortant cumulée pour la session en cours
##### Indicateur
###### outbound_contact_duration
- valeur par défault = '0'
- unité = seconde
- la durée start à remote_connected
- la durée stop à connection.disconnected

#### Durée moyenne du temps de contact avec les cibles sortantes pour la journée en cours
##### Indicateur
- utilise outbound_contact_duration

#### Durée maximum atteinte de contact avec une cible sortante sur la journée en cours
##### Indicateur
- utilise outbound_contact_duration

### Indicateurs communication
#### Identifiant de l'appel (call-id)
##### Indicateur
##### outbound_call_id (value=str)
- valeur par défault = ''
- suite à un progressing.invite si le state est outbound et sur la leg remote = 'call_xxxx@...'
- suite à outbound_cancel = ''
- suite à un connection.disconnected (normal et sortant) = ''
- suite à un connection.failed = ''

#### Chronomètre de durée totale
##### Indicateur
###### last_outbound_call_start
- valeur par défault = stop
- suite à un progressing.invite si le state est outbound et sur la leg remote = iso_now()
- suite à outbound_cancel = stop
- suite à un connection.disconnected (normal et sortant) = stop
- suite à un connection.failed = stop

#### Chronomètre de durée de contact
##### Indicateur
###### last_outbound_call_contact_start
- valeur par défault = stop
- suite à un remote_connected = iso_now()
- suite à un connection.disconnected = stop
- suite à task.outbound.dial = remote_display_name (provided when the ccxml client dial a number)

#### Login de l'agent qui a initié l'appel
##### Indicateur
###### last_outbound_call_target
- valeur par défault = ""
- suite à un connection.disconnect = ""
- suite à un connection.failed = ""
- suite à un outbound.cancel = ""