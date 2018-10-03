---
title: Cuadro de diálogo Propiedades de conexión (SSAS - Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.ConnectionProperties.F1
ms.assetid: 17bae8ae-2ba0-4978-be70-61c687f59d54
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8057222588cb388eafcb3e3bf1bd6daec443cca6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077295"
---
# <a name="connection-properties-dialog-box-ssas---tabular"></a>Propiedades de conexión (cuadro de diálogo) (SSAS: tabular)
  Utilice esta página para ver o modificar en SQL Server Management Studio las propiedades de conexión de un origen de datos que usa una base de datos modelo tabular.  
  
 Este cuadro de diálogo proporciona marcas de tiempo y otra información descriptiva, además de propiedades personalizables que determinan las características de la conexión.  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**Nombre**|Especifica el nombre del origen de datos.|  
|**ID**|Muestra el identificador del objeto de origen de datos.|  
|**Descripción**|Muestra la descripción del objeto de origen de datos.|  
|**Marca de tiempo de creación**|Muestra la fecha y hora en que se creó la base de datos.|  
|**Última actualización de esquema**|Muestra la fecha y hora en que se actualizaron por última vez los metadatos de la base de datos.|  
|**Cadena de conexión**|Muestra la cadena de conexión utilizada para conectarse al origen de datos que proporciona datos al modelo.|  
|**Número máximo de conexiones**|Especifica el número máximo de conexiones de cliente para esta base de datos.|  
|**Aislamiento**|Los valores válidos son ReadCommitted o Snapshot. Para más información, vea [Elemento de aislamiento &#40;ASSL&#41;](scripting/properties/isolation-element-assl.md).|  
|**Tiempo de espera de la consulta**|Especifica el tiempo, en segundos, después del que se agotará el tiempo de espera si se intentan recuperar los datos.|  
|**Proveedor administrado**|Especifica el nombre del proveedor administrado. Si la conexión de origen de datos usa un proveedor OLE DB nativo, este valor está vacío.|  
|**Información de suplantación**|Especifica la cuenta de suplantación que se usa en las conexiones a bases de datos al procesar o actualizar los datos, las consultas que se ejecutan en un almacén de datos relacional (mediante DirectQuery), los enlaces fuera de línea, las particiones remotas y la sincronización de bases de datos del destino al origen.<br /><br /> Los valores válidos incluyen la cuenta de servicio de Analysis Services o un conjunto específico de credenciales de Windows. No especifique **Usar las credenciales del usuario actual** o **Heredar**. Esas opciones de credenciales no se admiten para una base de datos de modelo tabular.|  
  
  
