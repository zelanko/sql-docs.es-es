Buscar errores de hardware Ejecute el diagnóstico de hardware y solucione cualquier problema. Examine también los registros del sistema y de aplicaciones de Windows, así como el registro de errores de SQL Server para ver si el error se produjo como resultado de un error de hardware. Corrija cualquier problema relacionado con el hardware que encuentre en los registros.

Si sigue teniendo problemas de datos dañados, intente intercambiar diferentes componentes de hardware para aislar el problema. Asegúrese de que el sistema no tiene habilitada la memoria caché de escritura en el controlador de disco. Si sospecha que el problema se debe a la caché de escritura, póngase en contacto con su proveedor de hardware.

Finalmente, puede resultarle útil cambiar a un nuevo sistema de hardware. Este cambio puede incluir volver a formatear las unidades de disco y volver a instalar el sistema operativo.

Restaurar desde una copia de seguridad Si el problema no está relacionado con el hardware y tiene disponible una copia de seguridad limpia, restaure la base de datos a partir de la copia de seguridad.

Ejecutar DBCC CHECKDB Si no hay una copia de seguridad limpia disponible, ejecute DBCC CHECKDB sin una cláusula REPAIR para determinar el alcance de los daños. DBCC CHECKDB recomendará el uso de una cláusula REPAIR. A continuación, ejecute DBCC CHECKDB con la cláusula REPAIR apropiada para reparar el problema.

> **no se admite la etiqueta de alerta**
> **no se admite la etiqueta tr**
> **no se admite la etiqueta tr**

Si ejecuta DBCC CHECKDB con una de las cláusulas REPAIR y no se soluciona el problema, póngase en contacto con su proveedor principal de soporte.

