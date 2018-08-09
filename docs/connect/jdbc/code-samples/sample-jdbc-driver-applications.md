---
title: Aplicaciones del controlador JDBC de ejemplo | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e136b87c-a138-45d6-8c3e-bcef94b7e483
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c62942580b403bbacd62c6fc65e0a19b0960f1e6
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39457819"
---
# <a name="sample-jdbc-driver-applications"></a>Aplicaciones del controlador JDBC de ejemplo

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Las aplicaciones de ejemplo [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] muestran varias características del controlador JDBC. Además, muestran las prácticas recomendadas de programación que puede aplicar al usar el controlador JDBC con una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
Todas las aplicaciones de ejemplo se incluyen en archivos de código *.java que se pueden compilar y ejecutar en el equipo local, y se encuentran en varias subcarpetas de la siguiente ubicación:  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples  
```

 En los temas de esta sección se describe cómo configurar y ejecutar las aplicaciones de ejemplo, y se incluye una descripción de lo que demuestran.  
  
## <a name="in-this-section"></a>En esta sección  
  
| Tema                                                                                                                  | Descripción                                                                                                                                                                                                                                                                   |
| ---------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Conexión y recuperación de datos](../../../connect/jdbc/code-samples/connecting-and-retrieving-data.md)                              | Estas aplicaciones de ejemplo demuestran cómo conectarse a una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Además, explican los distintos modos en los que se pueden recuperar datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. |
| [Trabajar con tipos de datos &#40;JDBC&#41;](../../../connect/jdbc/code-samples/working-with-data-types-jdbc.md)                        | Estas aplicaciones de ejemplo demuestran cómo usar los métodos de tipos de datos del controlador JDBC para trabajar con los datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].                                                                                              |
| [Trabajo con conjuntos de resultados](../../../connect/jdbc/code-samples/working-with-result-sets.md)                                          | Estas aplicaciones de ejemplo demuestran cómo usar los conjuntos de resultados para procesar los datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].                                                                                                            |
| [Trabajo con datos grandes](../../../connect/jdbc/code-samples/working-with-large-data.md)                                            | Estas aplicaciones de ejemplo demuestran cómo usar el almacenamiento en búfer adaptable para recuperar datos de valores grandes de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] sin la sobrecarga que suponen los cursores de servidor.                                                         |
| [Clasificación y detección de datos de SQL](../../jdbc/code-samples/data-discovery-and-classification-sample.md) | Esta aplicación de ejemplo muestra cómo recuperar información de clasificación y detección de datos contenida en un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos de un objeto de conjunto de resultados mediante el controlador JDBC.                                            |
  
## <a name="see-also"></a>Ver también

[Introducción al controlador JDBC](../../../connect/jdbc/overview-of-the-jdbc-driver.md)