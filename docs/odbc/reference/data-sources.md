---
title: Orígenes de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 92b8ca2b8c780e48cd9f3bf815ca86e3bd27081e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135630"
---
# <a name="data-sources"></a>Orígenes de datos
Un *origen de datos* es simplemente el origen de los datos. Puede ser un archivo, una base de datos determinada en un DBMS, o incluso una fuente de datos en directo. Los datos es posible que se encuentra en el mismo equipo que el programa, o en otro equipo en alguna parte de una red. Por ejemplo, un origen de datos podría ser un DBMS de Oracle que se ejecutan en un sistema de operativo OS/2®, accediendo a® de Novell Netware; un DBMS de DB2 de IBM que tiene acceso a través de una puerta de enlace; una colección de archivos de Xbase en un directorio de servidor. o un archivo de base de datos local de Microsoft® Access.  
  
 El propósito de un origen de datos es reunir toda la información técnica necesaria para acceder a los datos: nombre del controlador, dirección de red, software de red etc. - en un solo lugar y se oculta al usuario. El usuario debe ser capaz de ver una lista que incluye nóminas, inventario y personal, elija nóminas en la lista y tiene la aplicación conectarse a los datos de nóminas, todo sin conocer donde residen los datos de nóminas o cómo la aplicación llegó a él.  
  
 El término *origen de datos* no debe confundirse con condiciones similares. En este manual, *DBMS* o *base de datos* hace referencia a un motor o un programa de base de datos. Se hace una distinción más entre *bases de datos de escritorio,* está diseñado para ejecutarse en equipos personales y a menudo escaso en SQL completo y compatibilidad con transacciones, y *bases de datos del servidor,* diseñado para ejecutarse en un cliente / situación de servidor y se caracteriza por un motor de base de datos independiente y SQL enriquecida y compatibilidad con transacciones. *Base de datos* también hace referencia a una colección determinada de datos, como una colección de archivos de Xbase en un directorio o una base de datos en SQL Server. Generalmente es equivalente al término de *catálogo,* utilizados en este manual, o el término *calificador* en versiones anteriores de ODBC.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de orígenes de datos](../../odbc/reference/types-of-data-sources.md)  
  
-   [Usar orígenes de datos](../../odbc/reference/using-data-sources.md)  
  
-   [Ejemplo de origen de datos](../../odbc/reference/data-source-example.md)
