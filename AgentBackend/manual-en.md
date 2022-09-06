# Manual of backstage

## Profile of agent

The personal profile is shown on the `Account Management/Profile` page. If you'd like to see the downline agents' profile, please go to the `Account Management/Agent Management` page.

- Percentage: Take the percentage of profit which is the win/loss of members, the rest would be given to the upline
- Banned country: The IPs can not enter the game in the banned counties list
- Transaction method: Cash(transfer wallet) or seamless wallet
- Currency and quota: The sum of wins form members. Members of the agent won't take bets if over the quota limit. The the quota limit would be reset at 00:00:00 on the first day of every month(UTC+8), the downline agents also take the quota of upline
- Default currency: Every agent has one default currency. If there is no currency parameter in request when invoking our apis, our system will use the default currency of the agent.
- Whitelist IP: The ip form the request of the agent must in the whitelist IP list when invoking our apis(* sign means all ips are allowed from the request of the agent)

## Game setting of agent

Personal Game Setting is shown on the `Account Management/Personal Game Setting` page. If you'd like to see the downline agents' game setting, please go to the `Account Management/Agent Management` page.

- Activate game: Disallow to deactivate. The game/member/table limit/logo/seamless callbacks setting need to activate the game first
- Table setting: Please refer to the table No. from our game UI. Members of the agent won't enter the game table if disable the table No.. The game tables which disabled also won't be shown in game lobby
- Seamless wallet setting: Set the seamless version and the seamless callbacks
- Table limit setting: Set the default table limit of the currency. If there is no table limit parameter(`LimitStake`) in request when invoking creating member api, our system will use the default table limit of the agent.
- Switch setting: Set the member login switch for downline agents. Members of the agent cannot login if disabled
- Percentage setting: Set the percentage of profit for downline agents. One future percentage available(undelivered), our systems calculate the last month of delivery report when the routine maintenance on the first Monday every month. This page also provides the last 6 percentage records which are delivered. Able to modify the last 3 delivered percentage and our system will recalculate the delivery report of the modified month.
- Member management: Show all the members of personal and downline agents, but only personal members allow to modify member status and table limit.

## Billing Account Management
Check the account inquiry, bet record, transfer record, delivery record

## Agent Administrator
The sub-account of agent. Using the role-based access control(RBAC) system which able to add/update role permissions and append the role to the agent administrator. Also able to set platform available of agents for the agent administrator. **The agent administrator can not get the agent's records(include bets, accounting, transfer, members, ...etc) without the agent's platform available permission.**

## System Management
Able to upload customized logos on the `System Setting` page. There are 3 different sizes of logos in the game

## Developer Zone
- Developer Document: The `API Host`, `Agent ID`, `Agent Key` and API docs
- Key Generator: Test the API Key, using to confirm the Key in the request


