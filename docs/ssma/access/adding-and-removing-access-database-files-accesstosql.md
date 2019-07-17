---
title: Agregar y quitar el acceso a archivos (AccessToSQL) de base de datos. | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- adding Access files
- adding and removing Access databases
- browsing Access metadata
- browsing metadata, Access databases
- connecting, Access databases
- databases
- files, adding and removing
- finding Access databases
- finding database files
- locating database files
- metadata
- metadata, browsing
- metadata, refreshing
- refreshing metadata
- removing Access files
- scanning for database files
- searching for database files
ms.assetid: e944c740-4c8a-4bc1-b0ed-be57bc06dced
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 39df13a3cab2d842a313ca37fc4a98d0c331ba83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104212"
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>Agregar y quitar archivos de base de datos de Access (AccessToSQL)
Para migrar datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, debe agregar uno o más bases de datos de Access al proyecto SSMA. Estas bases de datos deben ser Access 97 o versiones posteriores. Si tiene bases de datos desde una versión anterior de acceso, debe convertir las bases de datos a una versión más reciente. Para ello, abriendo y guardando las bases de datos en Access 97 o una versión posterior antes de agregarlos a SSMA.  
  
## <a name="what-happens-when-you-add-access-database-files"></a>¿Qué ocurre cuando se agregan archivos de base de datos de acceso?  
Al agregar una base de datos de Access a un proyecto SSMA, SSMA lee los metadatos de la base de datos y, a continuación, agrega estos metadatos al archivo de proyecto. Estos metadatos describen la base de datos y sus objetos. SSMA usa los metadatos cuando convierte objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sintaxis de SQL Azure, y cuando migra los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Puede examinar estos metadatos en el Explorador de metadatos de acceso y revisar las propiedades de objetos de base de datos individual.  
  
> [!NOTE]  
> Una base de datos de Access se puede dividir en varios archivos: una base de datos de back-end que contiene las tablas y bases de datos front-end que contienen consultas, formularios, informes, macros, módulos y los accesos directos. Si desea migrar una base de datos división [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, agregue la base de datos front-end para SSMA.  
  
## <a name="permissions-that-are-required-by-ssma"></a>Permisos necesarios de SSMA  
Para migrar una base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, el grupo de usuarios y el usuario administrador deben tener permisos de administración. Para obtener información sobre cómo migrar bases de datos con protección de grupo de trabajo, consulte [preparar bases de datos de Access para la migración](preparing-access-databases-for-migration-accesstosql.md).  
  
## <a name="selecting-databases-to-add"></a>Seleccionar bases de datos para agregar  
Si desea agregar una o varias bases de datos a un proyecto SSMA, y los archivos están en una ubicación conocida, puede agregar los archivos mediante el procedimiento siguiente.  
  
**Para agregar archivos de base de datos individual**  
  
1.  En el **archivo** menú, haga clic en **agregar bases de datos**.  
  
2.  En el **abierto** diálogo cuadro, busque la carpeta que contiene el archivo de base de datos o archivos.  
  
3.  Seleccione los archivos que desea agregar y, a continuación, haga clic en **abierto**.  
  
## <a name="finding-databases-to-add"></a>Buscar bases de datos para agregar  
Si desea agregar varias bases de datos de Access desde diferentes carpetas a un proyecto de SSMA, o desea agregar un único archivo, pero tiene que buscar el archivo, puede seguir estos pasos para buscar uno de varios archivos y agregarlos al proyecto.  
  
**Para buscar y agregar las bases de datos**  
  
1.  En el **archivo** menú, haga clic en **buscar bases de datos**.  
  
2.  En el Asistente para buscar las bases de datos, escriba el nombre de la unidad, ruta de acceso de archivo o la ruta de acceso UNC que desea buscar. Como alternativa, haga clic en **examinar** para buscar la carpeta de red o la unidad.  
  
3.  Haga clic en **agregar** para agregar la ubicación a la lista.  
  
    Repita los dos pasos anteriores para agregar más ubicaciones de búsqueda.  
  
4.  Opcionalmente, agregue los criterios de búsqueda para restringir la lista de bases de datos que se devuelven.  
  
    > [!IMPORTANT]  
    > El **todo o parte del nombre de archivo** cuadro de texto no admite caracteres comodín.  
  
5.  Haga clic en **Scan**.  
  
    Aparece la página de análisis. Esto muestra las bases de datos que se han encontrado y el progreso de la búsqueda. Para detener la búsqueda, haga clic en **detener**.  
  
6.  En la página Seleccionar archivos, seleccione las bases de datos que desea agregar al proyecto.  
  
    Puede usar el **seleccionar todo** y **Borrar todo** botones en la parte superior de la lista para seleccionar o borrar todas las bases de datos. Puede presionada la tecla CTRL para seleccionar varias bases de datos, o mantenga presionada la tecla MAYÚS hacia abajo para seleccionar un intervalo de bases de datos.  
  
7.  Haga clic en **Next**.  
  
8.  En la página de comprobación, haga clic en **finalizar**.  
  
## <a name="browsing-access-metadata"></a>Examinar los metadatos de acceso  
Después de agregar una base de datos de Access a un proyecto, los metadatos del proyecto aparecen en el Explorador de metadatos de acceso. Puede examinar la jerarquía de las bases de datos y objetos de base de datos en el explorador.  
  
**Para examinar los metadatos**  
  
1.  En el Explorador de metadatos de acceso, expanda **acceso de metabase**y, a continuación, expanda **bases de datos**.  
  
2.  Expanda la base de datos que desea revisar y, a continuación, expanda **consultas**.  
  
    Tenga en cuenta la lista de consultas. Si selecciona una consulta, un **SQL** ficha y un **propiedades** ficha aparece en el panel derecho.  
  
3.  Expanda **tablas** y, a continuación, seleccione una tabla.  
  
    Observe que aparecen cuatro pestañas: **Tabla**, **asignación de tipos de**, **propiedades**, y **datos**.  
  
4.  Expanda una tabla, **claves**y, a continuación, seleccione una clave.  
  
    Las propiedades de clave aparecen en el panel derecho.  
  
5.  Expanda **índices**y, a continuación, seleccione un índice.  
  
    Las propiedades de índice aparecen en el panel derecho.  
  
## <a name="refreshing-databases"></a>Actualizar las bases de datos  
Si una base de datos de Access cambia después de agregar el archivo, puede actualizar los metadatos de la base de datos de Access.  
  
**Para actualizar los metadatos de acceso**  
  
-   En el Explorador de metadatos de acceso, haga clic en la base de datos y, a continuación, seleccione **actualizar desde la base de datos**.  
  
## <a name="removing-databases"></a>Quitar bases de datos  
Puede quitar una base de datos de Access desde un proyecto siguiendo estos pasos.  
  
**Para quitar una base de datos de un proyecto**  
  
1.  En el Explorador de metadatos de acceso, expanda **acceso de metabase**y, a continuación, expanda **bases de datos**.  
  
2.  Haga clic en la base de datos y, a continuación, seleccione **Quitar base de datos**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [conectarse a SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Crear y administrar proyectos](creating-and-managing-projects-accesstosql.md)  
  
