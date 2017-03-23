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

#### Nombre de legs cibles tentées pour la journée en cours
##### Indicateur
###### total_leg_count
- valeur par défault = '0'
- incrémentation lors d'un remote_invite

#### Nombre de legs cibles contactées pour la journée en cours
##### Indicateur
###### contacted_leg_count
- valeur par défault = '0'
- incrémentation lors d'un remote_connected.

#### Nombre de legs cibles en échec pour la journée en cours
##### Indicateur
###### failed_leg_count
- valeur par défault = '0'
- incrémentation lors d'un connection.failed.

#### Nombre de legs cibles annulées pour la journée en cours
##### Indicateur
###### canceled_leg_count
- valeur par défault = '0'
- incrémentation lors d'un outbound_cancel

#### Durée en état sortant cumulée pour la journée en cours
##### Indicateur

#### Durée en contact sortant cumulée pour la journée en cours
##### Indicateur

#### Durée moyenne du temps de sonnerie des cibles sortantes pour la journée en cours
##### Indicateur

#### Durée moyenne du temps de contact avec les cibles sortantes pour la journée en cours
##### Indicateur

#### Durée moyenne du temps de mise en garde des cibles sortantes pour la journée en cours
##### Indicateur

#### Durée maximum atteinte de sonnerie d'une cible sortante sur la journée en cours
##### Indicateur

#### Durée maximum atteinte de contact avec une cible sortante sur la journée en cours
##### Indicateur

#### Durée maximum atteinte de mise en garde d'une cible sortante sur la journée cours
##### Indicateur

### Indicateurs communication
#### Date-heure de début de l'appel sortant en cours
##### Indicateur
###### outbound_call_start_time (value=str)
- valeur par défault = stop
- suite à un progressing.invite si le state est outbound et sur la leg remote = iso_now()
- suite à outbound_cancel = stop
- suite à un connection.disconnected (normal et sortant) = stop
- suite à un connection.failed = stop

#### Identifiant de l'appel (call-id)
##### Indicateur
##### outbound_call_id (value=str)
- valeur par défault = ''
- suite à un progressing.invite si le state est outbound et sur la leg remote = 'call_xxxx@...'
- suite à outbound_cancel = ''
- suite à un connection.disconnected (normal et sortant) = ''
- suite à un connection.failed = ''

#### Numéro cible et nom éventuel du contact
##### Indicateur
###### outbound_remote_name

#### Chronomètre de durée totale
##### Indicateur
###### outbound_call_start_time
- valeur par défault = stop
- suite à un progressing.invite si le state est outbound et sur la leg remote = iso_now()
- suite à outbound_cancel = stop
- suite à un connection.disconnected (normal et sortant) = stop
- suite à un connection.failed = stop

#### Chronomètre de durée de tentative d'appel
##### Indicateur
###### outbound_call_ringing_duration (value=str)
- valeur par défault = ""
- suite à un connection.connected sur la leg remote = "xx" (exemple: 22) 

#### Chronomètre de durée de contact
##### Indicateur
###### outbound_call_contact_duration
- valeur par défault = ""
- suite à un connection.disconnected sur la leg remote = "xx" (exemple: 67)

#### Login de l'agent qui a initié l'appel
##### Indicateur
###### outbound_source_login
- valeur par défault = ""


Indicateurs CCCP
===============
### Indicateurs agents
#### Nombre de legs cibles tentées pour la journée en cours
##### Indicateur
###### user_total_leg_count
- valeur par défault = 0
- est la somme de tout les total_leg_count sur 24h depuis les sessions.

#### Nombre de legs cibles contactées pour la journée en cours
##### Indicateur
###### user_contacted_leg_count
- valeur par défault = 0
- est la somme de tout les contacted_leg_count sur 24h depuis les sessions.
- 
#### Nombre de legs cibles en échec pour la journée en cours
##### Indicateur
###### user_failed_leg_count
- valeur par défault = 0
- est la somme de tout les failed_leg_count sur 24h depuis les sessions.

#### Nombre de legs cibles annulées pour la journée en cours
##### Indicateur
###### user_canceled_leg_count
- valeur par défault = 0
- est la somme de tout les canceled_leg_count sur 24h depuis les sessions.