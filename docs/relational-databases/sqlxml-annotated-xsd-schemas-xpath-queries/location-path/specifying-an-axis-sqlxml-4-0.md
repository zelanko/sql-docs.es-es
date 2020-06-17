---
title: Especificar un eje (SQLXML)
description: Obtenga información sobre cómo especificar un eje en una consulta XPath de SQLXML 4,0 especifica la relación de árbol entre los nodos seleccionados por la fase de ubicación y el nodo de contexto.
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], axes
- XPath queries [SQLXML], location paths
- self axis
- attribute axis [SQLXML]
- axis [SQLXML]
- child axis
- parent axis
- location path for XPath query
- axes [SQLXML]
ms.assetid: 65631795-3389-40cf-90ea-85e9438956c5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 43daf972eacd67dcd7e75eabd1aca87bb3f67932
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84882183"
---
# <a name="specifying-an-axis-sqlxml-40"></a>Especificar un eje (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
-   El eje especifica la relación jerárquica entre los nodos seleccionados por el paso de ubicación y el nodo de contexto. Se admiten los siguientes ejes: **secundarios**  
  
     Contiene el elemento secundario del nodo de contexto.  
  
     La expresión XPath siguiente (ruta de acceso de ubicación) selecciona del nodo de contexto actual todos los **\<Customer>** elementos secundarios:  
  
    ```  
    child::Customer  
    ```  
  
     En la consulta XPath siguiente, `child` es el eje. `Customer` es la prueba de nodo.  
  
-   **aérea**  
  
     Contiene el elemento primario del nodo de contexto.  
  
     La expresión XPath siguiente selecciona todos los **\<Customer>** elementos primarios de los **\<Order>** elementos secundarios:  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     Esto equivale a especificar `child::Customer`. En esta consulta XPath, `child` y `parent` son los ejes. `Customer` y `Order` son las pruebas de nodo.  
  
-   **attribute**  
  
     Contiene el atributo del nodo de contexto.  
  
     La expresión XPath siguiente selecciona el atributo **CustomerID** del nodo de contexto:  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   **mismo**  
  
     Contiene el propio nodo de contexto.  
  
     La expresión XPath siguiente selecciona el nodo actual si es el **\<Order>** nodo:  
  
    ```  
    self::Order  
    ```  
  
     En esta consulta XPath, `self` es el eje y `Order` es la prueba de nodo.  
  
  
