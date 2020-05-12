Quita un grupo de cargas de trabajo del regulador de recursos definido por el usuario existente.

![Icono de vínculo de tema](../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintaxis

```syntaxsql
DROP WORKLOAD GROUP group_name
[;]
```

## <a name="arguments"></a>Argumentos

*nombre_de_grupo* es el nombre de un grupo de cargas de trabajo definido por el usuario existente.

## <a name="remarks"></a>Observaciones

La instrucción DROP WORKLOAD GROUP no se permite en los grupos predeterminados o internos del regulador de recursos.

Si va a ejecutar instrucciones de DDL, se recomienda familiarizarse primero con los estados del regulador de recursos. Para obtener más información, vea [Resource Governor](../relational-databases/resource-governor/resource-governor.md).

Si un grupo de cargas de trabajo contiene sesiones activas, no se podrá quitar ni mover el grupo de cargas de trabajo a otro grupo de recursos de servidor si se llama a la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE para aplicar el cambio. Para evitar este problema, puede realizar una de las siguientes acciones:

- Espere hasta que se hayan desconectado todas las sesiones en el grupo afectado y, a continuación, vuelve a ejecutar la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE.

- Detenga explícitamente las sesiones en el grupo afectado mediante el comando KILL y, a continuación, vuelva a ejecutar la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE.

- Reinicie el servidor. Una vez completado el proceso del reinicio, no se creará el grupo eliminado y un grupo movido utilizará la nueva asignación del grupo de recursos de servidor.

- En un escenario en el que ha emitido la instrucción DROP WORKLOAD GROUP pero no desea detener explícitamente las sesiones para aplicar el cambio, puede recrear el grupo si utiliza el mismo nombre que tenía antes de emitir la instrucción DROP y, a continuación, mueve el grupo al grupo de recursos de servidor original. Para aplicar los cambios, ejecute la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE.

## <a name="permissions"></a>Permisos

Requiere el permiso CONTROL SERVER.

## <a name="examples"></a>Ejemplos

En el ejemplo siguiente se quita el grupo de cargas de trabajo denominado `adhoc`.

```
DROP WORKLOAD GROUP adhoc;
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>Consulte también

- [Regulador de recursos](../relational-databases/resource-governor/resource-governor.md)
- [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-workload-group-transact-sql.md)  
- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../t-sql/statements/alter-resource-governor-transact-sql.md)  