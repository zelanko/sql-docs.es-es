---
title: 'Vincular aplicaciones de Access a SQL Server: base de datos SQL de Azure | Microsoft Docs'
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, linking to SQL Azure
- Access databases, linking to SQL Server
- auto-increment columns
- data types, unsupported
- hyperlink columns
- linking tables
- migrating databases, post-migration issues
- post-migration issues
- reference, post-migration issues
- refreshing linked tables
- slow performance
- unlinking tables
ms.assetid: 82374ad2-7737-4164-a489-13261ba393d4
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 61558536574750e7588124afb75cf26ee580b22a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47701513"
---
# <a name="linking-access-applications-to-sql-server---azure-sql-db-accesstosql"></a>Vinculación de aplicaciones de acceso a SQL Server: Azure SQL DB (AccessToSQL)
Si desea usar las aplicaciones de Access existentes con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede vincular las tablas de Access originales a la que se migrado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tablas de SQL Azure. Vinculación modifica la base de datos de acceso para que las páginas de acceso a las consultas, formularios, informes y datos usan los datos en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o base de datos de SQL Azure en lugar de los datos de la base de datos de Access.  
  
> [!NOTE]  
> Las tablas de Access permanecen en el acceso, pero no se actualizan junto con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o las actualizaciones de SQL Azure. Después de vincular las tablas y comprobar la funcionalidad, es posible que desee eliminar las tablas de Access.  
  
## <a name="linking-access-and-sql-server-tables"></a>Vincular tablas de Access y SQL Server  
Cuando se vincula una tabla de Access a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tabla de SQL Azure, el motor de base de datos Jet almacena información de conexión y los metadatos de la tabla, pero los datos se almacenan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Esta vinculación permite que las aplicaciones de Access funcionan con el acceso a tablas, aunque la tablas reales y los datos están en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
> [!NOTE]  
> Si usas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, la contraseña se almacena en texto no cifrado en las tablas vinculadas de acceso. Se recomienda usar la autenticación de Windows.  
  
**Vincular tablas**  
  
1.  En el Explorador de metadatos de acceso, seleccione las tablas que desea vincular.  
  
2.  Haga clic en **tablas**y, a continuación, seleccione **vínculo**.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) para el acceso se realiza una copia de seguridad de la tabla de acceso original y crea una tabla vinculada.  
  
Después de vincular las tablas, las tablas de SSMA aparecen con un icono de vínculo pequeño. En Access, aparecen las tablas con un icono "vinculado", que es un mundo con una flecha que apunta a ella.  
  
Al abrir una tabla en Access, los datos se recuperan mediante un cursor keyset. Como resultado, para tablas grandes, todos los datos no se recuperan al mismo tiempo. Sin embargo, durante la navegación a través de la tabla, Access recupera datos adicionales según sea necesario.  
  
> [!IMPORTANT]  
> Para vincular las tablas de access con una base de datos de Azure, necesita Client(SNAC) nativo de SQL Server versión 10.5 o posterior.   
> Puede obtener la última versión de SNAC desde [Microsoft® SQL Server® 2008 R2 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=196940).  
  
## <a name="unlinking-access-tables"></a>Desvinculando las tablas de Access  
Al desvincular una tabla de Access desde un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tabla de SQL Azure, SSMA restaura la tabla de acceso original y sus datos.  
  
**Para desvincular tablas**  
  
1.  En el Explorador de metadatos de acceso, seleccione las tablas que desea desvincular.  
  
2.  Haga clic en **tablas**y, a continuación, seleccione **desvincular**.  
  
## <a name="linking-tables-to-a-different-server"></a>Vincular tablas en un servidor diferente  
Si ha vinculado el acceso a tablas a una instancia de SQL Server y posteriormente desea cambiar los vínculos a otra instancia, debe volver a vincular las tablas.  
  
**Vincular tablas en un servidor diferente**  
  
1.  En el Explorador de metadatos de acceso, seleccione las tablas que desea desvincular.  
  
2.  Haga clic en **tablas** y, a continuación, seleccione **desvincular**.  
  
3.  Haga clic en el **volver a conectar a SQL Server** botón.  
  
4.  Conéctese a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure a la que desea vincular las tablas de Access.  
  
5.  En el Explorador de metadatos de acceso, seleccione las tablas que desea vincular.  
  
6.  Haga clic en **tablas**y, a continuación, seleccione **vínculo**.  
  
## <a name="updating-linked-tables"></a>Actualizar las tablas vinculadas  
Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o se modifican las definiciones de tabla de SQL Azure, puede desvincular y, a continuación, volver a vincular las tablas de SSMA mediante los procedimientos que se mostró anteriormente en este tema. También puede actualizar las tablas mediante el acceso.  
  
**Para actualizar las tablas vinculadas mediante el acceso**  
  
1.  Abra la base de datos de Access.  
  
2.  En el **objetos** lista, haga clic en **tablas**.  
  
3.  Haga clic en una tabla vinculada y, a continuación, seleccione **Administrador de tablas vinculadas**.  
  
4.  Active la casilla situada junto a cada tabla vinculada a la que desea actualizar y, a continuación, haga clic en **Aceptar**.  
  
## <a name="possible-post-migration-issues"></a>Posibles problemas posteriores a la migración  
Las siguientes secciones de problemas de la lista que se produzcan en aplicaciones de Access existentes después de migrar las bases de datos de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure y, a continuación, vincular las tablas, junto con las causas y las resoluciones.  
  
### <a name="slow-performance-with-linked-tables"></a>Rendimiento lento con tablas vinculadas  
**Causa:** algunas consultas podrían ser lentos después de convertir a SQL Server por las razones siguientes:  
  
-   La aplicación depende de las funciones que no existen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, lo que hace que Jet que desplegar tablas localmente para ejecutar una consulta SELECT.  
  
-   Las consultas que actualizan o eliminan el número de filas se envían por Jet como una consulta parametrizada para cada fila.  
  
**Solución:** convertir las consultas de ejecución lenta en vistas, procedimientos almacenados o consultas de paso a través. Convertir en consultas de paso tiene los siguientes problemas:  
  
-   No se puede modificar las consultas de paso a través. Modificar el resultado de la consulta o agregar nuevos registros debe realizarse en un procedimiento alternativo, como al tener explícita **modificar** o **agregar** botones en el formulario que está enlazado a la consulta.  
  
-   Algunas consultas requieren la intervención del usuario, pero las consultas de paso a través no admiten la entrada del usuario. Entrada del usuario se puede obtener Visual Basic para aplicaciones (VBA) que el código solicite los parámetros, o bien un formulario que se utiliza como un control de entrada. En ambos casos, el código de VBA envía la consulta con la entrada del usuario en el servidor.  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>Columnas de incremento automático no se actualizan hasta que se actualiza el registro  
**Causa:** después de llamar a RecordSet.AddNew de Jet, la columna de incremento automático está disponible antes de actualiza el registro. Esto no es cierto en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. El nuevo valor del valor de columna de identidad nueva está disponible solo después de guardar el nuevo registro.  
  
**Solución:** ejecute el siguiente código Visual Basic para aplicaciones (VBA) antes de obtener acceso al campo de identidad:  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>No hay disponibles nuevos registros  
**Causa:** al agregar un registro a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o una tabla de SQL Azure mediante el uso de VBA, si el campo de índice único de la tabla tiene un valor predeterminado y no asigna un valor para ese campo, el nuevo registro no aparece hasta que vuelva a la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o S SQL Azure. Si se intenta obtener un valor desde el nuevo registro, recibirá el mensaje de error siguiente:  
  
`Run-time error '3167' Record is deleted.`  
  
**Solución:** al abrir el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure de la tabla mediante el uso de código de VBA, incluya el `dbSeeChanges` opción, como en el ejemplo siguiente:  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>Tras la migración, algunas consultas no permitirá al usuario agregar un nuevo registro  
**Causa:** si una consulta no incluye todas las columnas que se incluyen en un índice único, no se puede agregar nuevos valores mediante el uso de la consulta.  
  
**Solución:** asegurarse de que todas las columnas incluidas en al menos un índice único forman parte de la consulta.  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>No se puede modificar un esquema de tabla vinculada con acceso  
**Causa:** después de la migración de datos y tablas de vinculación, el usuario no puede modificar el esquema de una tabla de Access.  
  
**Solución:** modificar el esquema de tabla mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y, a continuación, actualice el vínculo de acceso.  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>Se pierde la funcionalidad de hipervínculo después de migrar datos  
**Causa:** después de migrar datos, los hipervínculos en columnas pierden su funcionalidad y se convierten en simple **nvarchar (max)** columnas.  
  
**Solución:** ninguno.  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>No se admiten algunos tipos de datos de SQL Server por acceso  
**Causa:** si más tarde actualiza su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tablas de SQL Azure para que contenga los tipos de datos que no son compatibles con el acceso, no se puede abrir la tabla en Access.  
  
**Solución:** puede definir una consulta de acceso que devuelve solo aquellas filas que contienen tipos de datos admitidos.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
