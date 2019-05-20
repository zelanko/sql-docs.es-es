---
title: Crear base de datos (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3b051e5f2dc951eb07d4a23a5a22e15f1b2cc071
ms.sourcegitcommit: 8d288ca178e30549d793c40510c4e1988130afb0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65805125"
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>Crear base de datos (Asistente para importación y exportación de SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Si selecciona **Nuevo** en la página **Seleccionar un destino** para crear una base de datos de destino de SQL Server nueva, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra el cuadro de diálogo **Crear base de datos** . En esta página, debe proporcionar un nombre para la base de datos nueva. Si quiere, también puede cambiar la configuración del tamaño inicial y el crecimiento automático de la nueva base de datos y su archivo de registro. 

En el cuadro de diálogo **Crear base de datos** del asistente solo se proporcionan las opciones básicas disponibles para crear una base de datos de SQL Server. Para ver y configurar todas las opciones de una base de datos nueva de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para crear la base de datos o configurarla una vez la haya creado el asistente. 

> [!NOTE]
> Si busca información sobre la instrucción CREATE DATABASE de [!INCLUDE[tsql](../../includes/tsql-md.md)] y no sobre el cuadro de diálogo **Crear base de datos** del Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  

## <a name="screen-shot-of-the-create-database-page"></a>Captura de pantalla de la página Crear base de datos  
En la siguiente captura de pantalla se muestra el cuadro de diálogo **Crear base de datos** del asistente.  

![Página Crear base de datos del Asistente para importación y exportación](../../integration-services/import-export-data/media/create-database.png "Create database page of the Import and Export Wizard")  

## <a name="provide-a-name-for-the-new-database"></a>Proporcionar un nombre para la nueva base de datos  
**Nombre**  
 Proporcione un nombre para la base de datos de destino de SQL Server.
 
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

## <a name="whats-next"></a>¿Qué sigue?  
 Después de proporcionar un nombre para la base de datos que creará el asistente y de hacer clic en **Aceptar**, el cuadro de diálogo **Crear base de datos** mostrará la página **Seleccionar un destino** . Para más información, vea [Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).  

