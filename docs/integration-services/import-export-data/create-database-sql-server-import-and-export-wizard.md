---
title: Crear base de datos (SQL Server importar y exportar) | Documentos de Microsoft
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3f8c2b652515f4c84121dcf14371a9e86c8f86f2
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="create-database-sql-server-import-and-export-wizard"></a>Crear base de datos (Asistente para importación y exportación de SQL Server)
Si selecciona **Nuevo** en la página **Seleccionar un destino** para crear una base de datos de destino de SQL Server nueva, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra el cuadro de diálogo **Crear base de datos** . En esta página, debe proporcionar un nombre para la base de datos nueva. Si quiere, también puede cambiar la configuración del tamaño inicial y el crecimiento automático de la nueva base de datos y su archivo de registro. 

El **Create Database** cuadro de diálogo del asistente ofrece solo las opciones básicas que están disponibles para crear una nueva base de datos de SQL Server. Para ver y configurar todas las opciones para un nuevo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la base de datos, use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para crear la base de datos, o para configurar la base de datos después de que el asistente crea uno. 

> [!NOTE]
> Si busca información sobre la instrucción CREATE DATABASE de [!INCLUDE[tsql](../../includes/tsql-md.md)] y no sobre el cuadro de diálogo **Crear base de datos** del Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  

## <a name="screen-shot-of-the-create-database-page"></a>Captura de pantalla de la página Crear base de datos  
En la siguiente captura de pantalla se muestra el cuadro de diálogo **Crear base de datos** del asistente.  

![Crear página de base de datos de la importación y el Asistente para exportación de](../../integration-services/import-export-data/media/create-database.png "Crear página de base de datos de la importación y el Asistente para exportación")  

## <a name="provide-a-name-for-the-new-database"></a>Proporcionar un nombre para la nueva base de datos  
**Nombre**  
 Proporcione un nombre para la base de datos de SQL Server de destino.
 
### <a name="naming-requirements"></a>Requisitos de nomenclatura
Cuando asigne un nombre a la base de datos, asegúrese de respetar las convenciones de nomenclatura de SQL Server.  
  
-   El nombre de la base de datos debe ser único en una instancia de SQL Server.  
  
-   El nombre de la base de datos puede tener un máximo de 123 caracteres. (Permite 5 caracteres para los sufijos que SQL Server anexa al archivo de datos y el archivo de registro, con un máximo de 128 caracteres).  
  
-   El nombre de la base de datos debe ajustarse a las reglas de los identificadores de SQL Server. Estos son los requisitos más importantes.  
  
    -   El primer carácter debe ser una letra, un carácter de subrayado (_), una arroba (@) o un signo de número (#).  
  
    -   Los caracteres siguientes pueden ser letras, números, una arroba, un signo de dólar ($), signo de número o un carácter de subrayado.  
  
    -   No se pueden usar espacios ni otros caracteres especiales.  
  
Para obtener información detallada sobre estos requisitos, vea [Identificadores de base de datos](../../relational-databases/databases/database-identifiers.md).  

## <a name="optionally-specify-data-file-and-log-file-options"></a>Opcionalmente, especifique opciones del archivo de registro y del archivo de datos

> [!TIP]
> Debe proporcionar un nombre para la base de datos nueva en el campo **Nombre** , pero normalmente puede dejar el tamaño de archivo y el crecimiento de archivo en sus valores predeterminados.

### <a name="data-file-options"></a>Opciones de archivo de datos  
 **Tamaño inicial**  
 Especifique el número de megabytes para el tamaño inicial del archivo de datos.  
  
 **No se permite el crecimiento**  
 Indique si el archivo de datos puede aumentar de tamaño más allá del tamaño inicial especificado.  
  
 **Crecimiento por porcentaje**  
 Especifique un porcentaje por el cual el archivo de datos puede aumentar de tamaño.  
  
 **Crecimiento por tamaño**  
 Especifique un número de megabytes por el cual el archivo de datos puede aumentar de tamaño.  
  
### <a name="log-file-options"></a>Opciones del archivo de registro  
 **Tamaño inicial**  
 Especifique el número de megabytes para el tamaño inicial del archivo de registro.  
  
 **No se permite el crecimiento**  
 Indique si el archivo de registro puede aumentar de tamaño, más allá del tamaño inicial especificado.  
  
 **Crecimiento por porcentaje**  
 Especifique un porcentaje por el cual el archivo de registro puede aumentar de tamaño.  
  
 **Crecimiento por tamaño**  
 Especifique un número de megabytes por el cual el archivo de registro puede aumentar de tamaño.  

### <a name="more-info"></a>Más información
Para obtener más información sobre las opciones de tamaño de archivo que aparecen en esta página, vea [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md). 

## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de proporcionar un nombre para la base de datos que creará el asistente y de hacer clic en **Aceptar**, el cuadro de diálogo **Crear base de datos** mostrará la página **Seleccionar un destino** . Para más información, vea [Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).  


