---
title: Instrucciones y limitaciones de SQLXML 4.0
description: Obtenga información sobre las instrucciones y las limitaciones del trabajo con SQLXML 4,0.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, about SQLXML
ms.assetid: fe433d30-90a1-421e-85c6-af13294dc18d
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 305565d542144a7e6e24663aadba1fb56a67eddb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97431398"
---
# <a name="guidelines-and-limitations-of-sqlxml-40"></a>Instrucciones y limitaciones de SQLXML 4.0
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Recuerde lo siguiente cuando trabaje con SQLXML 4.0:  
  
-   El código XML devuelto como resultado de una consulta no se valida con el esquema de asignación que generó el código XML.  
  
-   SQLXML 4.0 incluye PROGID independientes y dependientes de la versión. Se recomienda que todas las aplicaciones de producción utilicen PROGID dependientes de la versión. Esto es especialmente importante porque SQLXML 4.0 no es totalmente compatible con versiones anteriores. El uso de PROGID dependientes de la versión impide que se produzcan errores de producción al instalar nuevas versiones. El comportamiento del programa puede cambiar de una versión a otra por una serie de motivos, como la corrección de errores, posibles cambios en el diseño, etc. El uso de PROGID dependientes de la versión impide que se produzcan errores inesperados al instalar nuevas versiones. Con los PROGID dependientes de la versión, al instalar una nueva versión, la aplicación seguirá funcionando sin errores. Si decide cambiar los PROGID dependientes de versiones anteriores y utilizar los PROGID dependientes de la última versión en una nueva versión, debe probar la aplicación antes de llevarla a producción. Por ejemplo, las aplicaciones que utilizan PROGID independientes de la versión podrían producir un error en las siguientes situaciones:  
  
     Ejecuta una aplicación que utiliza SQLXML 4.0 y PROGID independientes de la versión y decide instalar otro programa de software. Este programa podría instalar una versión anterior de SQLXML. Se puede producir un error en la aplicación porque los PROGID independientes de la versión de la aplicación apuntarán ahora a la versión anterior de SQLXML, que puede o no puede tener la característica SQLXML que utiliza la aplicación.  
  
-   Si por alguna razón no desea utilizar el proveedor SQLXMLOLEDB y, en su lugar, desea usar el proveedor SQLOLEDB para las características SQLXML, establezca la propiedad **versión de SQLXML** en "SQLXML. 4.0".  
  
  
