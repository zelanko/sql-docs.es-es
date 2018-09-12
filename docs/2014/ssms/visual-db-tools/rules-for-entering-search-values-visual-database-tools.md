---
title: Reglas para especificar valores de búsqueda (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- time [SQL Server], searches
- date searches
- dates [SQL Server], searches
- embedding apostrophes [SQL Server]
- logical value searches [SQL Server]
- case-sensitive search matches
- search criteria [SQL Server], rules
- text value searches [SQL Server]
- numeric value searches [SQL Server]
ms.assetid: 3c8134b7-83f4-41b4-99c8-e3949a685ff5
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 44f1cc4f153ee340377ff3bbb7c8e692d3a7c041
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43809071"
---
# <a name="rules-for-entering-search-values-visual-database-tools"></a>Reglas para especificar valores de búsqueda (Visual Database Tools)
  En este tema se tratan las convenciones que se deben utilizar para especificar los siguientes tipos de valores literales en una condición de búsqueda:  
  
-   Valores de texto  
  
-   Valores numéricos  
  
-   Fechas  
  
-   Valores lógicos  
  
> [!NOTE]  
>  La información de este tema se deriva de las reglas para SQL 92 estándar. Sin embargo, cada base de datos puede implementar SQL a su forma. Por tanto, estas instrucciones podrían no ser válidas en algunos casos. Si tiene dudas sobre cómo se escriben valores de búsqueda en una base de datos específica, consulte la documentación de la base de datos.  
  
## <a name="searching-on-text-values"></a>Buscar valores de texto  
 Las siguientes directrices se aplican al escribir valores de texto en las condiciones de búsqueda:  
  
-   **Comillas** Escriba los valores de texto entre comillas sencillas, como en el siguiente ejemplo de apellido:  
  
    ```  
    'Smith'  
    ```  
  
     Cuando escriba una condición de búsqueda en el [panel Criterios](visual-database-tools.md), solo tiene que escribir el valor del texto; el Diseñador de consultas y vistas agregará automáticamente las comillas sencillas.  
  
    > [!NOTE]  
    >  En algunas bases de datos, los términos entre comillas sencillas se interpretan como valores literales, mientras que los términos entre comillas dobles se interpretan como objetos de base de datos, como las referencias a tablas o columnas. Por tanto, aunque el Diseñador de consultas y vistas puede aceptar términos entre comillas dobles, se podrían interpretar de una forma distinta de la esperada.  
  
-   **Apóstrofos incrustados** Si los datos que busca contienen una comilla sencilla (un apóstrofo), puede escribir dos comillas sencillas para indicar que lo que desea indicar con la comilla sencilla es un valor literal y no un delimitador. Por ejemplo, la siguiente condición busca el valor "Swann's Way":  
  
    ```  
    ='Swann''s Way'  
    ```  
  
-   **Límites de longitud** No exceda la longitud máxima de la instrucción SQL en la base de datos al escribir cadenas largas.  
  
-   **Distinción entre mayúsculas y minúsculas** Debe tener en cuenta las reglas de distinción de mayúsculas y minúsculas de la base de datos que esté usando. Esta base de datos determinará si las búsquedas de texto distinguen mayúsculas de minúsculas. Por ejemplo, algunas bases de datos interpretan que el operador "=" implica una coincidencia de mayúsculas y minúsculas, pero otras permiten coincidencias de cualquier combinación de caracteres en mayúsculas y minúsculas.  
  
     Si no está seguro de que la base de datos distinga mayúsculas de minúsculas en las búsquedas, puede utilizar las funciones UPPER o LOWER en la condición de búsqueda para convertir las mayúsculas y minúsculas de los datos de búsqueda, como se indica en el siguiente ejemplo:  
  
    ```  
    WHERE UPPER(lname) = 'SMITH'  
    ```  
  
## <a name="searching-on-numeric-values"></a>Buscar valores numéricos  
 Las siguientes directrices se aplican al escribir valores numéricos en las condiciones de búsqueda:  
  
-   **Comillas** No debe escribir números entre comillas.  
  
-   **Caracteres no numéricos** No incluya caracteres no numéricos, salvo el separador decimal (el definido en el cuadro de diálogo **Configuración regional** del Panel de control de Windows) y el signo negativo (-). No incluya símbolos de agrupación de dígitos (como el punto entre los millares) ni símbolos de moneda.  
  
-   **Separadores decimales** Si escribe números enteros, puede incluir un separador decimal, independientemente de si el valor que busca es un número entero o real.  
  
-   **Notación científica** Puede utilizar la notación científica para escribir números muy grandes o muy pequeños, como en el siguiente ejemplo:  
  
    ```  
    > 1.23456e-9  
    ```  
  
## <a name="searching-on-dates"></a>Buscar fechas  
 El formato empleado para escribir fechas dependerá de la base de datos utilizada y del panel del Diseñador de consultas y vistas en el que escriba la fecha.  
  
> [!NOTE]  
>  Si no sabe qué formato utiliza el origen de datos, escriba una fecha en la columna Filtro del panel Criterios en cualquier formato. El diseñador convertirá la mayoría de estas entradas al formato adecuado.  
  
 El Diseñador de consultas y vistas permite trabajar con los siguientes formatos de fecha:  
  
-   **Específico de la configuración regional** Formato especificado para las fechas en el cuadro de diálogo **Propiedades de la Configuración regional de Windows** .  
  
-   **Específico de la base de datos** Cualquier formato válido para la base de datos.  
  
-   **Fecha ANSI estándar** Formato que utiliza llaves, el marcador 'd' para designar la fecha y una cadena de fecha, como en el siguiente ejemplo:  
  
    ```  
    { d '1990-12-31' }  
    ```  
  
-   **Fecha y hora ANSI estándar** Similar a la fecha ANSI estándar, pero utiliza 'ts' en lugar de 'd' y agrega horas, minutos y segundos a la fecha (con un reloj de 24 horas), como en el siguiente ejemplo del 31 de diciembre de 1990:  
  
    ```  
    { ts '1990-12-31 00:00:00' }  
    ```  
  
     En general, las bases de datos que representan las fechas mediante un tipo de datos de fecha real utilizan el formato de fecha estándar ANSI. En cambio, las bases de datos que admiten un tipo de datos datetime utilizan el formato de fecha y hora.  
  
 En la tabla siguiente se resumen los formatos de fecha que se pueden utilizar en los distintos paneles del Diseñador de consultas y vistas.  
  
|**Panel**|**Formato de fecha**|  
|--------------|---------------------|  
|Criterios|Específico de la configuración regional Específico de la base de datos Estándar ANSI<br /><br /> Las fechas escritas en el [panel Criterios](visual-database-tools.md) se convierten a un formato compatible con la base de datos en el panel SQL.|  
|SQL|Específico de la base de datos Estándar ANSI|  
|Resultado|Específico de la configuración regional|  
  
## <a name="searching-on-logical-values"></a>Buscar valores lógicos  
 El formato de los datos lógicos varía de una base de datos a otra. Los valores False suelen almacenarse como cero (0). Un valor True se suele almacenar como 1 y, de vez en cuando, como -1. Las siguientes directrices se aplican al escribir valores lógicos en las condiciones de búsqueda:  
  
-   Para buscar un valor False, utilice un cero, como se indica en el siguiente ejemplo:  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 0  
    ```  
  
-   Si no está seguro del formato que debe utilizar al buscar un valor True, pruebe a utilizar 1, como se indica en el siguiente ejemplo:  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 1  
    ```  
  
-   Como alternativa, puede ampliar el ámbito de la búsqueda a cualquier valor distinto de cero, como se indica en el siguiente ejemplo:  
  
    ```  
    SELECT * FROM authors  
    WHERE contract <> 0  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Especificar criterios de búsqueda (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)  
  
  
