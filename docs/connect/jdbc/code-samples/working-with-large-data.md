---
title: Trabajar con datos de gran tamaño | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9269200560447593a50364a4b4801a8ec80f4ca
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39455269"
---
# <a name="working-with-large-data"></a>Trabajar con datos grandes

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

El controlador JDBC proporciona compatibilidad con el almacenamiento en búfer adaptable, que le permite recuperar cualquier tipo de datos de valores grandes sin sufrir la sobrecarga de los cursores de servidor. Con el almacenamiento en búfer adaptable, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] recupera los resultados de la ejecución de una instrucción de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] a medida que la aplicación los necesita, en lugar de todos a la vez. El controlador también descarta los resultados en cuanto la aplicación ya no puede tener acceso a ellos.  
  
En la versión 1.2 del controlador JDBC de [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)], el modo de almacenamiento en búfer predeterminado es "**full**". Si la aplicación no estableció la propiedad de conexión "responseBuffering" en "**adaptive**" bien en las propiedades de conexión o utilizando el método [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) del objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), el controlador admitirá leer de una sola vez el resultado completo desde el servidor. Para obtener el comportamiento de almacenamiento en búfer adaptable, su aplicación tenía que establecer explícitamente la propiedad de conexión "responseBuffering" en "**adaptive**".  
  
El valor **adaptive** es el modo predeterminado de almacenamiento en búfer y el controlador JDBC almacena en búfer los datos mínimos posibles cuando es necesario. Para obtener más información sobre el uso de almacenamiento en búfer adaptable, vea [usando almacenamiento en búfer adaptable](../../../connect/jdbc/using-adaptive-buffering.md).  
  
En los temas de esta sección se describen las distintas formas en que puede usar datos de valores grandes desde una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
  
| Tema                                                                                                                         | Descripción                                                              |
| ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| [Lectura de un ejemplo de datos grandes](../../../connect/jdbc/code-samples/reading-large-data-sample.md)                                               | Describe cómo usar una instrucción SQL para recuperar datos de valores grandes.       |
| [Lectura de datos grandes con un ejemplo de procedimientos almacenados](../../../connect/jdbc/code-samples/reading-large-data-with-stored-procedures-sample.md) | Describe cómo recuperar un valor de parámetro CallableStatement OUT grande. |
| [Actualización de un ejemplo de datos grandes](../../../connect/jdbc/code-samples/updating-large-data-sample.md)                                             | Describe cómo actualizar datos de valor grande en una base de datos.                |
  
## <a name="see-also"></a>Ver también

[Aplicaciones del controlador JDBC de ejemplo](../../../connect/jdbc/code-samples/sample-jdbc-driver-applications.md)  
  