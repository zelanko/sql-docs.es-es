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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14499071bd180a7ea709fda3eb26aeae46f229c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077021"
---
# <a name="data-returned-by-catalog-functions"></a>Datos devueltos por las funciones de catálogo
Cada función de catálogo devuelve datos como un conjunto de resultados. Este conjunto de resultados no es diferente de cualquier otro conjunto de resultados. Por lo general se genera por predefinido, parametrizada **seleccione** instrucción que está codificado de forma rígida en el controlador o están almacenados en un procedimiento en el origen de datos. Para obtener información acerca de cómo recuperar datos de un conjunto de resultados, vea [fue un resultado se establece crean?](../../../odbc/reference/develop-app/was-a-result-set-created.md).  
  
 El conjunto de resultados para cada función de catálogo se describen en la entrada de referencia para esa función. Además de las columnas enumeradas, el conjunto de resultados puede contener columnas específicas del controlador después de la última columna predefinida. Estas columnas (si existe) se describen en la documentación del controlador.  
  
 Las aplicaciones deben enlazar las columnas específicas del controlador en relación con el final del conjunto de resultados. Es decir, debe calcular el número de columna específicos del controlador como el número de la última columna - recuperado con **SQLNumResultCols** : menos el número de columnas que se producen después de la columna obligatoria. Esto ahorra tener que cambiar la aplicación cuando se agregan nuevas columnas al resultado establecido en futuras versiones de ODBC o el controlador. Para que este esquema para que funcione, los controladores deben agregar nuevas columnas específicas del controlador antes de columnas específicas del controlador anteriores para que los números de columna no cambian en relación con el final del conjunto de resultados.  
  
 Los identificadores que se devuelven en el conjunto de resultados no están entre comillas, incluso si contienen caracteres especiales. Por ejemplo, suponga que el identificador de carácter de comilla (que es específico del controlador y se devuelven a través de **SQLGetInfo**) es un signo de comillas doble (") y la tabla de cuentas por pagar contiene una columna denominada Customer Name. En la fila devuelta por **SQLColumns** para esta columna, el valor de la columna TABLE_NAME es cuentas por pagar, no "cuentas por pagar", y el valor de la columna COLUMN_NAME es el nombre de cliente, no "Customer Name". Para recuperar los nombres de los clientes en la tabla de cuentas por pagar, la aplicación podría incluir los nombres de estos:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 Para obtener más información, consulte [identificadores entre comillas](../../../odbc/reference/develop-app/quoted-identifiers.md).  
  
 Las funciones de catálogo se basan en un modelo de autorización similar a SQL en el que se realiza una conexión en función de un nombre de usuario y una contraseña y se devuelven solo los datos para el que el usuario tiene el privilegio. Protección con contraseña de los archivos individuales, que no encajan en este modelo, es definido por el controlador.  
  
 Los conjuntos de resultados devueltos por las funciones de catálogo casi nunca son actualizables y las aplicaciones no deben esperar para que pueda cambiar la estructura de la base de datos cambiando los datos de estos conjuntos de resultados.
