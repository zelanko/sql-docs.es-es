---
title: Datos devueltos por las funciones de catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0d9b63de04f79fd95c1b06d8e84d85c6f4fea02
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305238"
---
# <a name="data-returned-by-catalog-functions"></a>Datos devueltos por las funciones de catálogo
Cada función de catálogo devuelve los datos como un conjunto de resultados. Este conjunto de resultados no es diferente de ningún otro conjunto de resultados. Normalmente se genera mediante una instrucción **Select** parametrizada predefinida que está codificada de forma rígida en el controlador o almacenada en un procedimiento en el origen de datos. Para obtener información sobre cómo recuperar datos de un conjunto de resultados, vea ¿ [se ha creado un conjunto de resultados?](../../../odbc/reference/develop-app/was-a-result-set-created.md).  
  
 El conjunto de resultados de cada función de catálogo se describe en la entrada de referencia de esa función. Además de las columnas enumeradas, el conjunto de resultados puede contener columnas específicas del controlador después de la última columna predefinida. Estas columnas (si las hay) se describen en la documentación del controlador.  
  
 Las aplicaciones deben enlazar columnas específicas del controlador con respecto al final del conjunto de resultados. Es decir, deben calcular el número de una columna específica del controlador como el número de la última columna recuperada con **SQLNumResultCols** -menos el número de columnas que aparecen después de la columna requerida. Esto evita tener que cambiar la aplicación cuando se agregan nuevas columnas al conjunto de resultados en versiones futuras de ODBC o del controlador. Para que este esquema funcione, los controladores deben agregar nuevas columnas específicas del controlador antes que las columnas específicas del controlador anterior, de modo que los números de columna no cambien en relación con el final del conjunto de resultados.  
  
 Los identificadores que se devuelven en el conjunto de resultados no se incluyen entre comillas, aunque contengan caracteres especiales. Por ejemplo, supongamos que el carácter de comilla de identificador (que es específico del controlador y que se devuelve a través de **SQLGetInfo**) es una comilla doble (") y la tabla cuentas por pagar contiene una columna denominada nombre del cliente. En la fila devuelta por **SQLColumns** para esta columna, el valor de la columna TABLE_NAME es Accounts Payable, no "Accounts Payable" y el valor de la columna column_name es Customer Name, no "Customer Name". Para recuperar los nombres de los clientes de la tabla Accounts Payable, la aplicación comillasa de estos nombres:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 Para obtener más información, vea [identificadores entre comillas](../../../odbc/reference/develop-app/quoted-identifiers.md).  
  
 Las funciones de catálogo se basan en un modelo de autorización similar a SQL en el que se realiza una conexión basada en un nombre de usuario y contraseña, y solo se devuelven los datos para los que el usuario tiene un privilegio. La protección mediante contraseña de archivos individuales, que no caben en este modelo, está definida por el controlador.  
  
 Los conjuntos de resultados devueltos por las funciones de catálogo casi nunca se pueden actualizar, y las aplicaciones no deberían esperar poder cambiar la estructura de la base de datos cambiando los datos de estos conjuntos de resultados.
