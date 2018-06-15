---
title: Datos devueltos por las funciones de catálogo | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d27d395913ce64d263798205521a3d1136460105
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910580"
---
# <a name="data-returned-by-catalog-functions"></a>Datos devueltos por las funciones de catálogo
Cada función de catálogo devuelve datos como un conjunto de resultados. Este conjunto de resultados no es diferente de cualquier otro conjunto de resultados. Se genera normalmente por predefinido, con parámetros **seleccione** que esté almacenado en un procedimiento en el origen de datos o codificado de forma rígida en el controlador. Para obtener información acerca de cómo recuperar datos de un conjunto de resultados, vea [era un resultado se establece crean?](../../../odbc/reference/develop-app/was-a-result-set-created.md).  
  
 El conjunto de resultados para cada función de catálogo se describe en la entrada de referencia de dicha función. Además de las columnas enumeradas, el conjunto de resultados puede contener columnas específicas del controlador después de la última columna predefinida. Estas columnas (si existe) se describen en la documentación del controlador.  
  
 Las aplicaciones deben enlazar columnas específicas del controlador en relación con el final del conjunto de resultados. Es decir, debe calcular el número de columna específicos del controlador como el número de la última columna, se recuperan con **SQLNumResultCols** , menos el número de columnas que se producen después de la columna obligatoria. Este modo se ahorra tener que cambiar la aplicación cuando se agregan nuevas columnas al resultado establece en futuras versiones de ODBC o el controlador. Para que este esquema para que funcione, controladores deben agregar nuevas columnas específicas del controlador antes de las columnas específicas del controlador antiguas para que los números de columna no cambian con relación al final del conjunto de resultados.  
  
 Los identificadores que se devuelven en el conjunto de resultados no están entre comillas, aunque contengan caracteres especiales. Por ejemplo, suponga que el identificador de carácter de comillas (que es específico del controlador y se devuelven a través de **SQLGetInfo**) es un signo de comillas dobles (") y la tabla de cuentas por pagar contiene una columna denominada Customer Name. En la fila devuelta por **SQLColumns** para esta columna, el valor de la columna TABLE_NAME es cuentas por pagar, no "cuentas por pagar", y el valor de la columna COLUMN_NAME es el nombre de cliente, no "Customer Name". Para recuperar los nombres de clientes en la tabla de cuentas por pagar, la aplicación podría quote estos nombres:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 Para obtener más información, consulte [identificadores entrecomillados](../../../odbc/reference/develop-app/quoted-identifiers.md).  
  
 Las funciones de catálogo se basan en un modelo de autorización similar a SQL en el que se realiza una conexión en función de un nombre de usuario y una contraseña y se devuelven solo los datos para el que el usuario tiene un privilegio. Protección con contraseña de archivos individuales, que no se ajusta a este modelo, es definido por el controlador.  
  
 Los conjuntos de resultados devueltos por las funciones de catálogo casi nunca son actualizables y las aplicaciones no deben esperar para que pueda cambiar la estructura de la base de datos cambiando los datos de estos conjuntos de resultados.
