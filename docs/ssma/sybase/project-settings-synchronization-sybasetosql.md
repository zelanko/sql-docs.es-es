---
title: Configuración (sincronización) (SybaseToSQL) del proyecto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fcdcfc8d113bca42a9f042e8e6196d3de55b8e7e
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "40394507"
---
# <a name="project-settings-synchronization-sybasetosql"></a>Configuración del proyecto (sincronización) (SybaseToSQL)
La página de sincronización de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA carga los objetos de base de datos, como tablas y procedimientos almacenados, en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
Puede tener acceso a dos páginas diferentes de sincronización que contienen los mismos valores:  
  
-   Si desea especificar la configuración para todos los proyectos SSMA futuros, en el **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para los que es necesaria para ver o cambiar configuración desde **versión de destino de migración** lista desplegable y, a continuación, seleccione **sincronización** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración para el proyecto actual, en el **herramientas** menú, seleccione **configuración del proyecto**y, a continuación, seleccione **sincronización** en la parte inferior del panel izquierdo.  
  
## <a name="options"></a>Opciones  
**Intentos**  
Especifica el número de intentos de SSMA debe realizar cuando se carga en los objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los objetos que no se cargan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el intento actual volverá a intentarse hasta SSMA alcanza el número máximo de intentos en el proceso de sincronización actual.  
  
## <a name="synchronization-for-sql-server"></a>Sincronización de SQL Server  
**Actualizar objeto local en el cambio de los objetos locales y remotos**  
Especifica si SSMA debe reemplazar los metadatos del objeto local con los metadatos del objeto remoto si cambian los objetos locales y remotos.  
Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
Si selecciona **escribir en la base de datos**, SSMA actualizará los objetos de la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.   
Conjunto de opciones de forma predeterminada es **escribir en la base de datos.**  
  
**Actualizar un objeto local en el cambio de objeto local**  
Especifica si SSMA debe reemplazar los metadatos del objeto local con los metadatos del objeto remoto si cambia el objeto remoto.  
Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.   
Conjunto de opciones de forma predeterminada es **escribir en la base de datos**.  
  
**Actualizar un objeto local en el cambio de objeto remoto**  
Especifica si SSMA debe reemplazar los metadatos del objeto local con los metadatos del objeto remoto si cambia el objeto remoto.  
Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.   
Conjunto de opciones de forma predeterminada es **actualizar desde la base de datos**.  
  
**Actualizar cuando faltan los metadatos del objeto local**  
Especifica si SSMA debe crear los metadatos locales si existe un objeto en la base de datos de destino, pero no de forma local.  
Si selecciona **actualizar desde la base de datos**, SSMA selecciona la actualización de la opción de base de datos cuando se cumple la condición.  
Si selecciona **escribir en la base de datos**, SSMA eliminará el objeto de la base de datos cuando se cumple la condición.  
Si selecciona **Skip**, SSMA no realizará ninguna acción de actualización.   
Conjunto de opciones de forma predeterminada es **actualizar desde la base de datos**.  
  
