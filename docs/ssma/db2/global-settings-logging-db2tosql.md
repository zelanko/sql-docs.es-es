---
title: Configuración global (registro) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d314a2ca-ea2e-46e0-ae5e-8774841da91b
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7d632b040a5124d73470ce825af91e254866a0ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299216"
---
# <a name="global-settings-logging-db2tosql"></a>Configuración global (registro) (DB2ToSQL)
Use la **configuración Global** cuadro de diálogo para especificar la configuración de registro para SSMA. Normalmente, desea cambiar esta configuración solo cuando se trabaja con servicios de soporte técnico.  
  
Para obtener acceso a este cuadro de diálogo, en el **herramientas** menú, seleccione **configuración Global** y, a continuación, haga clic en el **registro** situado en la parte inferior del panel izquierdo.  
  
## <a name="options"></a>Opciones  
**Nivel de mensajes**  
Las siguientes opciones están disponibles en **mensajes nivel**:  
  
|Opción|Descripción|  
|----------|---------------|  
|**[todas las categorías]**|Se usa para establecer el nivel de registro para todas las opciones siguientes.|  
|**Collector**|Recopila metadatos sobre el esquema de origen y lo guarda en el proyecto.|  
|**Convertidor de tipos**|Convierte las estructuras de objetos de base de datos de origen, como tablas y procedimientos almacenados, en correspondiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estructuras.|  
|**Migrador de datos**|Migra los datos de la base de datos de origen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Formatter**|Subcomponente del convertidor que genera scripts para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema.|  
|**Interfaz gráfica de usuario**|Mensajes que aparecen cuando se usa la herramienta SSMA.|  
|**Linker**|Resuelve los identificadores de SQL y se proporciona información a otros componentes.|  
|**Otro**|Todos los mensajes que no están en cualquier otra categoría.|  
|**Parser**|Analiza el esquema de origen.|  
|**Sincronizador**|En los objetos de base de datos del origen de carga [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**TreeConverter**|Convierte los objetos en los metadatos de origen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadatos.|  
|**Herramienta de comprobación**|Mensajes que aparecen cuando se usa la herramienta de comprobación de SSMA.|  
  
En cada opción **mensajes nivel**, configure uno de los siguientes niveles de registro para SSMA:  
  
|||  
|-|-|  
|**Error irrecuperable**|Escribir solo mensajes de error grave en el registro.|  
|**Error**|Escribir error y mensajes de error grave en el registro.|  
|**Advertencia**|Escribir mensajes de error grave, error y advertencia en el registro.|  
|**Info**|Escribir informativo, advertencia, error y mensajes de error grave en el registro.|  
|**Depuración**|Escribir todos los mensajes, incluidos los mensajes, en el registro de depuración.|  
  
**Ruta de acceso de archivo de registro**  
La ruta de acceso y nombre de los archivos de registro SSMA. Para especificar un nombre diferente, haga clic en la ruta de acceso actual y, a continuación, haga clic en el ( **...** ) botón.  
  
**Tamaño del archivo de registro**  
El tamaño máximo del archivo de registro en KB. El tamaño mínimo es de 10 KB. El tamaño predeterminado es 10240 KB.  
  
**Número total de archivos de registro**  
Cuando se llena un registro, SSMA se cambie el nombre del archivo de registro y comenzar una nueva. Con esta configuración, especifique el número máximo de archivos de registro para mantener. El valor mínimo es 2.  
  
