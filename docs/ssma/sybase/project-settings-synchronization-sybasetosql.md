---
title: Configuración (sincronización) (SybaseToSQL) del proyecto | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49783b54640b82295b54450ad7eb63ea044e0721
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="project-settings-synchronization-sybasetosql"></a>Configuración del proyecto (la sincronización) (SybaseToSQL)
La página de sincronización de la **configuración del proyecto** cuadro de diálogo contiene opciones que personalizan la forma en que SSMA carga los objetos de base de datos, como tablas y procedimientos almacenados, en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure.  
  
Puede tener acceso a dos páginas diferentes de sincronización que contengan los mismos valores:  
  
-   Si desea especificar la configuración para todos los proyectos futuros de SSMA, en la **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para el que se requiere para puede ver o cambiar de configuración **versión de destino de migración** de lista desplegable y, a continuación, seleccione **sincronización** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración para el proyecto actual, en la **herramientas** menú, seleccione **configuración del proyecto**y, a continuación, seleccione **sincronización** en la parte inferior del panel izquierdo.  
  
## <a name="options"></a>Opciones  
**Intentos**  
Especifica el número de intentos de SSMA debe realizar cuando carga los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Objetos que no se cargan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en el intento actual se intentará de nuevo hasta que SSMA alcanza el número máximo de intentos en el proceso de sincronización actual.  
  
## <a name="synchronization-for-sql-server"></a>Sincronización para SQL Server  
**Actualizar un objeto local de cambio de objetos locales y remotos**  
Especifica si SSMA debe reemplazar los metadatos del objeto local con los metadatos del objeto remoto si cambian los objetos locales y remotos.  
Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
Si selecciona **escribir en la base de datos**, SSMA actualizará los objetos de la base de datos según el contenido de los metadatos SSMA cuando se cumpla la condición.  
Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.   
Conjunto de opciones de forma predeterminada es **escribir en la base de datos.**  
  
**Actualizar un objeto local en el cambio de objeto local**  
Especifica si SSMA debe reemplazar los metadatos del objeto local con los metadatos del objeto remoto si cambia el objeto remoto.  
Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.   
Conjunto de opciones de forma predeterminada es **escribir en la base de datos**.  
  
**Actualizar un objeto local en el cambio de objeto remoto**  
Especifica si SSMA debe reemplazar los metadatos del objeto local con los metadatos del objeto remoto si cambia el objeto remoto.  
Si selecciona **actualizar desde la base de datos**, SSMA cargará las definiciones de base de datos en los metadatos cuando se cumple la condición.  
Si selecciona **escribir en la base de datos**, SSMA actualizará el objeto en la base de datos según el contenido de los metadatos SSMA cuando se cumple la condición.  
Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.   
Conjunto de opciones de forma predeterminada es **actualizar desde la base de datos**.  
  
**Actualizar una vez que faltan metadatos del objeto local**  
Especifica si SSMA debe crear los metadatos locales si un objeto existe en la base de datos de destino, pero no de forma local.  
Si selecciona **actualizar desde la base de datos**, SSMA selecciona la actualización de la opción de base de datos cuando se cumple la condición.  
Si selecciona **escribir en la base de datos**, SSMA eliminará el objeto de la base de datos cuando se cumpla la condición.  
Si selecciona **omitir**, SSMA no llevará a cabo las acciones de actualización.   
Conjunto de opciones de forma predeterminada es **actualizar desde la base de datos**.  
  
