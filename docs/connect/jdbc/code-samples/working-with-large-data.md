---
title: "Trabajar con datos de gran tamaño | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 11a8f89d8e61a656f9328d83c8fd154351981718
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="working-with-large-data"></a>Trabajar con datos grandes
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  El controlador JDBC proporciona compatibilidad con el almacenamiento en búfer adaptable, que le permite recuperar cualquier tipo de datos de valores grandes sin sufrir la sobrecarga de los cursores de servidor. Con el almacenamiento en búfer adaptable, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] recupera los resultados de la ejecución de instrucción de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] como la aplicación los necesita, en lugar de todos a la vez. El controlador también descarta los resultados en cuanto la aplicación ya no puede tener acceso a ellos.  
  
 En el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)] versión 1.2 del controlador JDBC, el modo del almacenamiento en búfer era "**completa**" de forma predeterminada. Si la aplicación no estableció la propiedad de conexión "responseBuffering" "**adaptable**" en las propiedades de conexión o mediante el [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método de la [ SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) (objeto), el controlador admitidos leer el resultado completo desde el servidor a la vez. Para obtener el comportamiento de almacenamiento en búfer adaptable, su aplicación tenía que establezca la propiedad de conexión "responseBuffering" en "**adaptable**" explícitamente.  
  
 El **adaptable** el valor predeterminado es el modo de almacenamiento en búfer y el controlador JDBC almacena en búfer los datos mínimos posibles cuando sea necesario. Para obtener más información sobre el uso de almacenamiento en búfer adaptable, vea [usar almacenamiento en búfer adaptable](../../../connect/jdbc/using-adaptive-buffering.md).  
  
 Los temas de esta sección describen distintas formas en que puede usar para recuperar los datos de valores grandes de una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Ejemplo de lectura de datos de gran tamaño](../../../connect/jdbc/reading-large-data-sample.md)|Describe cómo usar una instrucción SQL para recuperar datos de valores grandes.|  
|[Leer datos de gran tamaño con un ejemplo de procedimientos almacenados](../../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md)|Describe cómo recuperar un valor de parámetro CallableStatement OUT grande.|  
|[Actualización de datos de gran tamaño de ejemplo](../../../connect/jdbc/updating-large-data-sample.md)|Describe cómo actualizar datos de valor grande en una base de datos.|  
  
## <a name="see-also"></a>Vea también  
 [Aplicaciones de controlador JDBC de ejemplo](../../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  

