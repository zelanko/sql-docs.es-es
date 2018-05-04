---
title: Orígenes de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 13f39771ed48501e4ab90494bdff9d3253219bba
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-sources"></a>Orígenes de datos
A *origen de datos* es simplemente el origen de los datos. Puede ser un archivo, una base de datos determinada en un DBMS, o incluso una fuente de datos en directo. Los datos podrían ser ubicados en el mismo equipo que el programa o en otro equipo en algún punto de una red. Por ejemplo, un origen de datos podría ser un DBMS de Oracle que se ejecuta en un sistema de operativo OS/2®, acceso Novell® Netware; un DBMS de DB2 de IBM que tiene acceso a través de una puerta de enlace; una colección de archivos de Xbase en un directorio del servidor; o un archivo de base de datos local de Microsoft® Access.  
  
 El propósito de un origen de datos es reunir toda la información técnica necesaria para tener acceso a los datos, el nombre del controlador, dirección de red, software de red y así sucesivamente, en una sola, colocar y ocultar del usuario. El usuario debe ser capaz de ver una lista que incluye nóminas, inventario y personal, elija nómina en la lista y hacer que la aplicación conectarse a los datos de nóminas, sin necesidad de conocer donde residen los datos de nóminas o cómo la aplicación llegó a él.  
  
 El término *origen de datos* no deben confundirse con condiciones similares. En este manual, *DBMS* o *base de datos* hace referencia a un motor o un programa de base de datos. Se realiza una diferencia adicional entre *bases de datos de escritorio,* está diseñado para ejecutarse en equipos personales y a menudo faltan en SQL completo y compatibilidad con transacciones, y *bases de datos de servidor,* diseñados para ejecutarse en un cliente / situación de servidor y caracterizado por un motor de base de datos independiente y SQL completo y compatibilidad con transacciones. *Base de datos* también hace referencia a una colección determinada de datos, como una colección de archivos de Xbase en un directorio o una base de datos en SQL Server. Es normalmente el equivalente al término *catálogo,* usa en otra parte en este manual, o bien, el término *calificador* en versiones anteriores de ODBC.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de orígenes de datos](../../odbc/reference/types-of-data-sources.md)  
  
-   [Usar orígenes de datos](../../odbc/reference/using-data-sources.md)  
  
-   [Ejemplo de origen de datos](../../odbc/reference/data-source-example.md)
