
<!--
### Code examples for Azure cloud differ slightly from on-premises
  Or.....
### Code examples can differ for Azure SQL Database
-->

Algunos ejemplos de código de Transact-SQL escritos para SQL Server local necesitan pequeños cambios para ejecutarse en el servicio Azure SQL Database en la nube. Una categoría de estos ejemplos de código implica vistas del sistema cuyos prefijos de nombre difieren ligeramente entre los dos sistemas de base de datos:

- **server\_** &nbsp; - &nbsp; _prefijo para el entorno local_
- **database\_** &nbsp; - &nbsp; _prefijo para el servicio Azure SQL DB en la nube_

Como ilustración, en la tabla siguiente se enumeran y comparan dos subconjuntos de las vistas del sistema. Por motivos de brevedad, los subconjuntos están restringidos a los nombres de vista que también contienen la cadena `_event`. Los subconjuntos tienen prefijos de nombre diferentes porque incluyen los dos sistemas de base de datos diferentes.

| Nombre del entorno local 2017 | Nombre del servicio en la nube |
| :------------------------- | :---------------------- |
| server_event_notifications<br />server_event_session_actions<br />server_event_session_events<br />server_event_session_fields<br />server_event_session_targets<br />server_event_sessions<br />server_events<br />server_trigger_events | database_event_session_actions<br />database_event_session_events<br />database_event_session_fields<br />database_event_session_targets<br />database_event_sessions |
| &nbsp; | &nbsp; |

Las dos listas de la tabla anterior son precisas a partir de junio del 2019. Pero el contenido de esta tabla puede quedar obsoleto, porque su contenido no se va a mantener. Para obtener listas precisas, ejecute la siguiente instrucción SELECT de T-SQL. Ejecute SELECT dos veces, una en cada sistema de base de datos.

```sql
SELECT name
    FROM sys.all_objects
    WHERE
        (name LIKE 'database\_%' { ESCAPE '\' } OR
         name LIKE 'server\_%' { ESCAPE '\' })
        AND name LIKE '%\_event%' { ESCAPE '\' }
        AND type = 'V'
    ORDER BY name;
```

<!--
The creation of this docs/includes/ file was prompted by Issue 2211 (https://github.com/MicrosoftDocs/sql-docs/issues/2211).
Initial PR was PR 10427 (https://github.com/MicrosoftDocs/sql-docs-pr/pull/10427).
The complaint was that a specific T-SQL code block failed on Azure SQL Database.

GeneMi  ,  2019/05/28
-->
