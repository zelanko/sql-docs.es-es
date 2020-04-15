---
title: Datos devueltos por las funciones del catálogo ( Catalog Functions) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305238"
---
# <a name="data-returned-by-catalog-functions"></a>Datos devueltos por las funciones de catálogo
Cada función de catálogo devuelve datos como un conjunto de resultados. Este conjunto de resultados no es diferente de cualquier otro conjunto de resultados. Normalmente se genera mediante una instrucción **SELECT** predefinida y parametrizada que está codificada de forma rígida en el controlador o almacenada en un procedimiento en el origen de datos. Para obtener información sobre cómo recuperar datos de un conjunto de resultados, vea [¿Se creó un conjunto](../../../odbc/reference/develop-app/was-a-result-set-created.md)de resultados? .  
  
 El conjunto de resultados para cada función de catálogo se describe en la entrada de referencia para esa función. Además de las columnas enumeradas, el conjunto de resultados puede contener columnas específicas del controlador después de la última columna predefinida. Estas columnas (si las hay) se describen en la documentación del controlador.  
  
 Las aplicaciones deben enlazar columnas específicas del controlador en relación con el final del conjunto de resultados. Es decir, deben calcular el número de una columna específica del controlador como el número de la última columna - recuperado con **SQLNumResultCols** - menos el número de columnas que se producen después de la columna necesaria. Esto ahorra tener que cambiar la aplicación cuando se agregan nuevas columnas al conjunto de resultados en versiones futuras de ODBC o el controlador. Para que este esquema funcione, los controladores deben agregar nuevas columnas específicas del controlador antes de las columnas antiguas específicas del controlador para que los números de columna no cambien en relación con el final del conjunto de resultados.  
  
 Los identificadores que se devuelven en el conjunto de resultados no se citan, incluso si contienen caracteres especiales. Por ejemplo, supongamos que el carácter de comillas de identificador (que es específico del controlador y se devuelve a través de **SQLGetInfo**) es una comilla doble (") y la tabla Proveedores contiene una columna denominada Nombre del cliente. En la fila devuelta por **SQLColumns** para esta columna, el valor de la columna TABLE_NAME es Proveedores, no "Cuentas por pagar", y el valor de la columna COLUMN_NAME es Nombre del cliente, no "Nombre del cliente". Para recuperar los nombres de los clientes en la tabla Proveedores, la aplicación citaría estos nombres:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 Para obtener más información, consulte [Identificadores entrecomillados](../../../odbc/reference/develop-app/quoted-identifiers.md).  
  
 Las funciones de catálogo se basan en un modelo de autorización similar a SQL en el que se realiza una conexión basada en un nombre de usuario y una contraseña, y solo se devuelven los datos para los que el usuario tiene privilegios. La protección con contraseña de archivos individuales, que no cabe en este modelo, está definida por el controlador.  
  
 Los conjuntos de resultados devueltos por las funciones de catálogo casi nunca son actualizables y las aplicaciones no deben esperar poder cambiar la estructura de la base de datos cambiando los datos de estos conjuntos de resultados.
