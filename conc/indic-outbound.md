Indicateurs agents
=================

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
- agent_connected: suite à connection.connected sur la leg agent, à la fin de la leg remote, et outbound_cancel.
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