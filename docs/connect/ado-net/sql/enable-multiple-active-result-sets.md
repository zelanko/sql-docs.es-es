---
title: Habilitación de conjuntos de resultados activos múltiples
description: Describe cómo usar MARS con SQL Server.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d0c40df5ec7648b7073f9efa369428b8d88f6d11
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452220"
---
# <a name="enabling-multiple-active-result-sets"></a>Habilitación de conjuntos de resultados activos múltiples

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Los conjuntos de resultados activos múltiples (MARS) son una característica que funciona con SQL Server y que permite la ejecución de varios lotes en una sola conexión. Cuando MARS está habilitado para su uso con SQL Server, cada objeto de comando usado agrega una sesión a la conexión.  
  
> [!NOTE]
>  Una sola sesión de MARS abre una conexión lógica para que MARS la use y, a continuación, una conexión lógica para cada comando activo.  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a>Habilitación y deshabilitación de MARS en la cadena de conexión  
  
> [!NOTE]
>  En las siguientes cadenas de conexión se usa la base de datos de ejemplo **AdventureWorks** que se incluye en SQL Server. Las cadenas de conexión proporcionadas suponen que la base de datos está instalada en un servidor llamado MSSQL1. Modifique la cadena de conexión según sea necesario para su entorno.  
  
La característica MARS está deshabilitada de forma predeterminada. Se puede habilitar agregando el par de palabras clave "MultipleActiveResultSets = True" a la cadena de conexión. "True" es el único valor válido para habilitar MARS. En el ejemplo siguiente se muestra cómo conectarse a una instancia de SQL Server y cómo especificar que se debe habilitar MARS. 
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
Puede deshabilitar MARS agregando el par de palabras clave "MultipleActiveResultSets = false" a la cadena de conexión. "False" es el único valor válido para deshabilitar MARS. La siguiente cadena de conexión muestra cómo deshabilitar MARS.  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a>Consideraciones especiales al usar MARS  
En general, no es necesario modificar las aplicaciones existentes para utilizar una conexión habilitada para MARS. Sin embargo, si desea usar las características de MARS en sus aplicaciones, debe comprender las siguientes consideraciones especiales.  
  
### <a name="statement-interleaving"></a>Intercalado de instrucciones  
Las operaciones MARS se ejecutan sincrónicamente en el servidor. Se permite la intercalación de instrucciones SELECT y BULK INSERT. Sin embargo, las instrucciones del lenguaje de manipulación de datos (DML) y del lenguaje de definición de datos (DDL) se ejecutan de forma atómica. Las instrucciones que intentan ejecutarse mientras se ejecuta un lote atómico están bloqueadas. La ejecución en paralelo en el servidor no es una característica de MARS.  
  
Si se envían dos lotes en una conexión MARS, uno de ellos que contiene una instrucción SELECT, el otro que contiene una instrucción DML, el DML puede empezar a ejecutarse dentro de la ejecución de la instrucción SELECT. Sin embargo, la instrucción DML debe ejecutarse hasta completarse antes de que la instrucción SELECT pueda progresar. Si ambas instrucciones se ejecutan en la misma transacción, los cambios realizados por una instrucción DML después de la ejecución de la instrucción SELECT no son visibles para la operación de lectura.  
  
Una instrucción WAITFOR dentro de una instrucción SELECT no produce la transacción mientras está en espera, es decir, hasta que se produce la primera fila. Esto implica que no se pueden ejecutar otros lotes dentro de la misma conexión mientras una instrucción WAITFOR está en espera.  
  
### <a name="mars-session-cache"></a>Caché de sesión de MARS  
Cuando se abre una conexión con MARS habilitado, se crea una sesión lógica que agrega sobrecarga adicional. Para minimizar la sobrecarga y mejorar el rendimiento, **SqlClient** almacena en caché la sesión MARS de una conexión. La memoria caché contiene como máximo 10 sesiones MARS. Este valor no es ajustable por el usuario. Si se alcanza el límite de la sesión, se crea una nueva sesión: no se genera un error. La memoria caché y las sesiones que contiene son por conexión; no se comparten entre las conexiones. Cuando se libera una sesión, se devuelve al grupo a menos que se haya alcanzado el límite superior del grupo. Si el grupo de caché está lleno, se cierra la sesión. Las sesiones de MARS no expiran. Solo se limpian cuando se desecha el objeto de conexión. La caché de la sesión de MARS no se ha cargado previamente. Se carga como la aplicación requiere más sesiones.  
  
### <a name="thread-safety"></a>Seguridad para subprocesos  
Las operaciones MARS no son seguras para subprocesos.  
  
### <a name="connection-pooling"></a>Agrupación de conexiones  
Las conexiones habilitadas para MARS se agrupan como cualquier otra conexión. Si una aplicación abre dos conexiones, una con MARS habilitado y otra con MARS deshabilitada, las dos conexiones se encuentran en grupos independientes.
  
### <a name="sql-server-batch-execution-environment"></a>Entorno de ejecución de batch de SQL Server  
Cuando se abre una conexión, se define un entorno predeterminado. A continuación, este entorno se copia en una sesión de MARS lógica.  
  
El entorno de ejecución por lotes incluye los siguientes componentes:  
  
- Opciones set (por ejemplo, ANSI_NULLS, DATE_FORMAT, LANGUAGE, TEXTSIZE)  
  
- Contexto de seguridad (rol de usuario/aplicación)  
  
- Contexto de base de datos (base de datos actual)  
  
- Variables de estado de ejecución (por ejemplo, @ @ERROR, @ @ROWCOUNT, @ @FETCH_STATUS @ @IDENTITY)  
  
- Tablas temporales de nivel superior  
  
Con MARS, un entorno de ejecución predeterminado está asociado a una conexión. Cada nuevo lote que empieza a ejecutarse en una conexión determinada recibe una copia del entorno predeterminado. Siempre que el código se ejecuta en un lote determinado, todos los cambios realizados en el entorno se limitan al lote específico. Cuando finaliza la ejecución, su configuración se copia en el entorno predeterminado. En el caso de un único lote que emite varios comandos para ejecutarse secuencialmente en la misma transacción, la semántica es la misma que la expuesta por las conexiones que implican clientes o servidores anteriores.  
  
### <a name="parallel-execution"></a>Ejecución en paralelo  
MARS no está diseñado para quitar todos los requisitos de varias conexiones en una aplicación. Si una aplicación necesita la verdadera ejecución en paralelo de comandos en un servidor, se deben usar varias conexiones.  
  
Por ejemplo, observe el siguiente escenario. Se crean dos objetos de comando, uno para procesar un conjunto de resultados y otro para actualizar los datos; comparten una conexión común a través de MARS. En este escenario, la transacción `Transaction`.`Commit` no puede realizar la actualización hasta que todos los resultados se han leído en el primer objeto de comando, lo que produce la siguiente excepción:  
  
Mensaje: Contexto de transacción en uso por otra sesión.  
  
Origen: proveedor de datos SqlClient de Microsoft  
  
Se esperaba: (NULL)  
  
Recibido: Microsoft. Data. SqlClient. SqlException  
  
Existen tres opciones para controlar este escenario:  
  
- Inicia la transacción una vez creado el lector, de modo que no forma parte de la transacción. Cada actualización se convierte entonces en su propia transacción.  
  
- Confirmar todo el trabajo después de cerrar el lector. Esto tiene la posibilidad de que un lote de actualizaciones sea considerable.  
  
- No usar MARS; en su lugar, use una conexión independiente para cada objeto de comando como lo haría antes de MARS.  
  
### <a name="detecting-mars-support"></a>Detección de compatibilidad con MARS  
Una aplicación puede comprobar la compatibilidad con MARS leyendo el valor de `SqlConnection.ServerVersion`. El número principal debe ser 9 para SQL Server 2005 y 10 para SQL Server 2008.  
  
## <a name="next-steps"></a>Pasos siguientes
- [Conjuntos de resultados activos múltiples (MARS)](multiple-active-result-sets-mars.md)
