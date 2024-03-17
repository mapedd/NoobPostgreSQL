# NoobPostgreSQL
Solutions to silly PosgreSQL problems

#1. Launching PosgreSQL servers
From what I can see, there are 3 popular ways of launching Postgres servers:
1. homebrew service
2. standalone binary
3. docker container
   
#2. Creating PosteSQL databases
#2. role "vapor_username" does not exist
```
[ WARNING ] PSQLError(code: server, serverInfo: [sqlState: 28000, file: miscinit.c, line: 756, message: role "vapor_username" does not exist, routine: InitializeSessionUserId, localizedSeverity: FATAL, severity: FATAL])
Swift/ErrorType.swift:200: Fatal error: Error raised at top level: PSQLError(code: server, serverInfo: [sqlState: 28000, file: miscinit.c, line: 756, message: role "vapor_username" does not exist, routine: InitializeSessionUserId, localizedSeverity: FATAL, severity: FATAL])
```
