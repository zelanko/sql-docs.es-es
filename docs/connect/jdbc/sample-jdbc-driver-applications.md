---
title: Aplicaciones del controlador JDBC de ejemplo | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e136b87c-a138-45d6-8c3e-bcef94b7e483
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f89bd1372735cf6656d2fcf6fc2da82ac69864a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745523"
---
# <a name="sample-jdbc-driver-applications"></a>Aplicaciones del controlador JDBC de ejemplo

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Las aplicaciones de ejemplo [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] muestran varias características del controlador JDBC. Además, muestran las prácticas recomendadas de programación que puede aplicar al usar el controlador JDBC con una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Todas las aplicaciones de ejemplo se incluyen en archivos de código *.java que se pueden compilar y ejecutar en el equipo local, y se encuentran en varias subcarpetas de la siguiente ubicación:  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples  
```

En los temas de esta sección se describe cómo configurar y ejecutar las aplicaciones de ejemplo, y se incluye una descripción de lo que demuestran.  
  
## <a name="in-this-section"></a>En esta sección  
  
| Tema                                                                                                        | Descripción                                                                                                                                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Conexión y recuperación de datos](../../connect/jdbc/connecting-and-retrieving-data.md)                       | Estas aplicaciones de ejemplo demuestran cómo conectarse a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Además, explican los distintos modos en los que se pueden recuperar datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. |
| [Trabajar con tipos de datos &#40;JDBC&#41;](../../connect/jdbc/working-with-data-types-jdbc.md)                 | Estas aplicaciones de ejemplo demuestran cómo usar los métodos de tipos de datos del controlador JDBC para trabajar con los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                           |
| [Trabajo con conjuntos de resultados](../../connect/jdbc/working-with-result-sets.md)                                   | Estas aplicaciones de ejemplo demuestran cómo usar los conjuntos de resultados para procesar los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                                         |
| [Trabajo con datos grandes](../../connect/jdbc/working-with-large-data.md)                                     | Estas aplicaciones de ejemplo demuestran cómo usar el almacenamiento en búfer adaptable para recuperar datos de valores grandes de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin la sobrecarga que suponen los cursores de servidor.                                                      |
| [Clasificación y detección de datos de SQL](../../connect/jdbc/data-discovery-classification-sample.md) | Esta aplicación de ejemplo muestra cómo recuperar información de clasificación y detección de datos contenida en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos de un objeto de conjunto de resultados mediante el controlador JDBC.                                      |
  
## <a name="see-also"></a>Ver también

[Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
