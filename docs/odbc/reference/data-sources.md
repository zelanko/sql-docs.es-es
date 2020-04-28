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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b7e464963471b0cad41c5b93d50507d0fa9bf96
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306516"
---
# <a name="data-sources"></a>Orígenes de datos
Un *origen de datos* es simplemente el origen de los datos. Puede ser un archivo, una base de datos determinada en un DBMS o incluso una fuente de distribución de datos activa. Los datos pueden estar ubicados en el mismo equipo que el programa o en otro equipo de una red. Por ejemplo, un origen de datos podría ser un DBMS de Oracle que se ejecute en un SO/2® sistema operativo, al que accede Novell® NetWare; un DBMS de IBM DB2 al que se tiene acceso a través de una puerta de enlace; colección de archivos xBase en un directorio del servidor; o un archivo de base de datos local de Microsoft® Access.  
  
 El propósito de un origen de datos es recopilar toda la información técnica necesaria para obtener acceso a los datos: el nombre del controlador, la dirección de red, el software de red, etc. en un solo lugar y ocultarlo al usuario. El usuario debe ser capaz de examinar una lista que incluya nóminas, inventario y personal, elegir nóminas en la lista y hacer que la aplicación se conecte a los datos de nóminas, todo ello sin saber dónde residen los datos de la nómina o cómo lo hizo la aplicación.  
  
 El término *origen de datos* no se debe confundir con términos similares. En este manual, *DBMS* o *base de datos* hace referencia a un programa o un motor de base de datos. Se realiza una distinción adicional entre *las bases de datos de escritorio,* diseñadas para ejecutarse en equipos personales y, a menudo, carecen de compatibilidad completa con SQL y transacciones, y con bases de datos de *servidor,* diseñadas para ejecutarse en una situación cliente/servidor y caracterizadas por un motor de base de datos independiente y la compatibilidad con transacciones y SQL enriquecidas. La *base* de datos también hace referencia a una colección determinada de datos, como una colección de archivos xBase en un directorio o en una base de datos de SQL Server. Por lo general, es equivalente al *Catálogo* de términos, que se usa en otra parte de este manual, o al término *calificador* en versiones anteriores de ODBC.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de orígenes de datos](../../odbc/reference/types-of-data-sources.md)  
  
-   [Usar orígenes de datos](../../odbc/reference/using-data-sources.md)  
  
-   [Ejemplo de origen de datos](../../odbc/reference/data-source-example.md)
