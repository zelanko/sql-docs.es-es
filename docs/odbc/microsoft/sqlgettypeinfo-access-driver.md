---
title: SQLGetTypeInfo (controlador de acceso) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLGetTypeInfo
- SQLGetTypeInfo function [ODBC], Access Driver
ms.assetid: a28b16eb-ca36-4297-9297-ecd7c107a84e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ddfa9bd29f0834adf1c211f9b8a111db0b94d3fe
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295155"
---
# <a name="sqlgettypeinfo-access-driver"></a>SQLGetTypeInfo (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El nombre del tipo (TYPE_NAME) devuelto en la tabla generada por **SQLGetTypeInfo** será el nombre más utilizado por el origen de datos.  
  
 SQL_ALL_EXCEPT_LIKE se devolverá en la columna SEARCHABLE para los tipos de datos Byte, Counter, Double, Single, Long y Short. (La capacidad LIKE se puede lograr convirtiendo el valor en un carácter mediante las funciones de conversión canónica ODBC y, a continuación, realizando la comparación.)
