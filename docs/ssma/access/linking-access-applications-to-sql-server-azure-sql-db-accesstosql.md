---
title: 'Vincular las aplicaciones de acceso a SQL Server: base de datos de SQL Azure | Documentos de Microsoft'
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: f33165118c2d7143ba75944b6515eca1338cce09
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="linking-access-applications-to-sql-server---azure-sql-db-accesstosql"></a>Vincular las aplicaciones de Access a SQL Server: base de datos de SQL de Azure (AccessToSQL)
Si desea usar las aplicaciones de Access existentes con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], puede vincular las tablas de Access originales a la migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tablas de SQL Azure. Vinculación modifica la base de datos de Access para que las páginas de acceso a las consultas, formularios, informes y datos usan los datos de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure en lugar de los datos de la base de datos de Access.  
  
> [!NOTE]  
> Las tablas de Access permanecen en Access, pero no se actualizan junto con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o las actualizaciones de SQL Azure. Después de vincular las tablas y comprobar la funcionalidad, puede eliminar las tablas de Access.  
  
## <a name="linking-access-and-sql-server-tables"></a>Vincular tablas de Access y SQL Server  
Cuando se vincula una tabla de Access a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tabla de SQL Azure, el motor de base de datos de Jet almacena información de conexión y metadatos de las tablas, pero los datos se almacenan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Esta vinculación permite que las aplicaciones de Access funcionan con las tablas de Access, aunque las tablas reales y los datos están en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure.  
  
> [!NOTE]  
> Si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticación, la contraseña se almacena en texto sin cifrar en las tablas vinculadas de Access. Se recomienda utilizar la autenticación de Windows.  
  
**Para vincular tablas**  
  
1.  En el Explorador de metadatos de acceso, seleccione las tablas que desea vincular.  
  
2.  Haga clic en **tablas**y, a continuación, seleccione **vínculo**.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) para acceso realiza una copia de seguridad de la tabla de acceso original y crea una tabla vinculada.  
  
Después de vincular las tablas, las tablas de SSMA aparecen con un icono de vínculo pequeño. En Access, las tablas aparecen con un icono de "vinculado", que es un globo terráqueo con una flecha que apunta a él.  
  
Cuando se abre una tabla en Access, los datos se recuperan mediante un cursor de conjunto de claves. Como resultado, para tablas grandes, todos los datos no se recuperan al mismo tiempo. Sin embargo, a medida que explora a través de la tabla, Access recupera datos adicionales según sea necesario.  
  
> [!IMPORTANT]  
> Para vincular las tablas de access con una base de datos de Azure, necesita SQL Server nativo Client(SNAC) versión 10.5 o posterior.   
> Puede obtener la última versión de SNAC de [Microsoft® SQL Server® 2008 R2 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=196940).  
  
## <a name="unlinking-access-tables"></a>Desvinculando acceso a tablas  
Al desvincular una tabla de Access desde un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tabla de SQL Azure, SSMA restaura la tabla de acceso original y sus datos.  
  
**Para desvincular tablas**  
  
1.  En el Explorador de metadatos de acceso, seleccione las tablas que desea desvincular.  
  
2.  Haga clic en **tablas**y, a continuación, seleccione **desvincular**.  
  
## <a name="linking-tables-to-a-different-server"></a>Vincular tablas en un servidor diferente  
Si ha vinculado las tablas de acceso a una instancia de SQL Server y más adelante desee cambiar los vínculos a otra instancia, debe volver a vincular las tablas.  
  
**Para vincular tablas en un servidor diferente**  
  
1.  En el Explorador de metadatos de acceso, seleccione las tablas que desea desvincular.  
  
2.  Haga clic en **tablas** y, a continuación, seleccione **desvincular**.  
  
3.  Haga clic en el **volver a conectar a SQL Server** botón.  
  
4.  Conéctese a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o a la que desea vincular el acceso a tablas de SQL Azure.  
  
5.  En el Explorador de metadatos de acceso, seleccione las tablas que desea vincular.  
  
6.  Haga clic en **tablas**y, a continuación, seleccione **vínculo**.  
  
## <a name="updating-linked-tables"></a>Actualizar tablas vinculadas  
Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o se modifican las definiciones de tabla de SQL Azure, puede desvincular y, a continuación, volver a vincular las tablas de SSMA mediante los procedimientos que se mostró anteriormente en este tema. También puede actualizar las tablas con el acceso.  
  
**Para actualizar las tablas vinculadas mediante el acceso**  
  
1.  Abra la base de datos de Access.  
  
2.  En el **objetos** lista, haga clic en **tablas**.  
  
3.  Haga clic en una tabla vinculada y, a continuación, seleccione **Administrador de tablas vinculadas**.  
  
4.  Active la casilla situada junto a cada tabla vinculada que desea actualizar y, a continuación, haga clic en **Aceptar**.  
  
## <a name="possible-post-migration-issues"></a>Posibles problemas posteriores a la migración  
Las siguientes secciones de problemas de la lista que se pueden producir en aplicaciones de Access existentes después de migrar las bases de datos de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure y, a continuación, vincular las tablas, junto con las causas y las resoluciones.  
  
### <a name="slow-performance-with-linked-tables"></a>Rendimiento lento con tablas vinculadas  
**Causa:** algunas consultas podrían ser lento después de convertir a SQL Server por los motivos siguientes:  
  
-   La aplicación depende de las funciones que no existen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, que hace que Jet descargar tablas localmente para ejecutar una consulta SELECT.  
  
-   Las consultas que actualizan o eliminan muchas filas se envían por Jet como una consulta parametrizada para cada fila.  
  
**Solución:** convertir las consultas de ejecución lenta en vistas, procedimientos almacenados o consultas de paso a través. Convertir en consultas de paso tiene los siguientes problemas:  
  
-   No se puede modificar las consultas de paso a través. Modificar el resultado de la consulta o agregar nuevos registros debe realizarse de una forma alternativa, como al tener explícita **modificar** o **agregar** botones en el formulario que está enlazado a la consulta.  
  
-   Algunas consultas requieren proporcionados por el usuario, pero las consultas de paso a través no admiten proporcionados por el usuario. Proporcionados por el usuario pueden obtenerse mediante Visual Basic para aplicaciones (VBA) que el código solicite los parámetros o mediante un formulario que se utiliza como un control de entrada. En ambos casos, el código VBA envía la consulta con la entrada del usuario en el servidor.  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>Columnas de incremento automático no se actualizan hasta que se actualiza el registro  
**Causa:** después de llamar a RecordSet.AddNew en Jet, la columna de incremento automático está disponible antes de actualiza el registro. Esto no es así en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. El nuevo valor de identidad columna nuevo valor está disponible sólo después de guardar el nuevo registro.  
  
**Solución:** ejecutar el siguiente ejemplo de Visual Basic para aplicaciones (VBA) antes de obtener acceso al campo de identidad:  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>No hay disponibles nuevos registros  
**Causa:** cuando se agrega un registro a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o una tabla de SQL Azure mediante el uso de VBA, si el campo de índice único de la tabla tiene un valor predeterminado y no asigna un valor a ese campo, el nuevo registro no aparece hasta que vuelva a abrir la tabla en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o S SQL Azure. Si se intenta obtener un valor desde el nuevo registro, recibirá el mensaje de error siguiente:  
  
`Run-time error '3167' Record is deleted.`  
  
**Solución:** al abrir el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure tabla mediante código VBA, incluya el `dbSeeChanges` opción, como en el ejemplo siguiente:  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>Tras la migración, algunas consultas no permitirá al usuario agregar un nuevo registro  
**Causa:** si una consulta no incluye todas las columnas que se incluyen en un índice único, no se puede agregar nuevos valores mediante el uso de la consulta.  
  
**Solución:** Asegúrese de que todas las columnas incluidas en al menos un índice único forman parte de la consulta.  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>No se puede modificar un esquema de tabla vinculada con acceso  
**Causa:** después de migrar los datos y tablas de vinculación, el usuario no puede modificar el esquema de una tabla de Access.  
  
**Solución:** modificar el esquema de tabla mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]y, a continuación, actualizar el vínculo de acceso.  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>Se pierde la funcionalidad de hipervínculo después de migrar datos  
**Causa:** después de migrar datos, los hipervínculos en columnas pierden su funcionalidad y se convierten en simples **nvarchar (max)** columnas.  
  
**Solución:** ninguno.  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>Algunos tipos de datos de SQL Server no son compatibles con acceso  
**Causa:** si más tarde actualiza su [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tablas de SQL Azure para contener los tipos de datos que no son compatibles con el acceso, no se puede abrir la tabla de Access.  
  
**Solución:** puede definir una consulta de acceso que devuelve solo aquellas filas que contienen tipos de datos admitidos.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
