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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306516"
---
# <a name="data-sources"></a>Orígenes de datos
Un origen de *datos* es simplemente el origen de los datos. Puede ser un archivo, una base de datos determinada en un DBMS o incluso una fuente de datos en tiempo real. Los datos pueden estar ubicados en el mismo equipo que el programa, o en otro equipo en algún lugar de una red. Por ejemplo, un origen de datos podría ser un DBMS de Oracle que se ejecuta en un sistema operativo OS/2®, al que novell ® Netware; un IBM DB2 DBMS al que se accede a través de una puerta de enlace; una colección de archivos Xbase en un directorio de servidor; o un archivo de base de datos local ® Access.  
  
 El propósito de una fuente de datos es recopilar toda la información técnica necesaria para acceder a los datos - el nombre del controlador, la dirección de red, el software de red, etc. - en un solo lugar y ocultarlo del usuario. El usuario debe poder ver una lista que incluya Nómina, Inventario y Personal, elegir Cálculo de nómina en la lista y hacer que la aplicación se conecte a los datos de nómina, todo ello sin saber dónde residen los datos de nómina ni cómo llegó la aplicación a ella.  
  
 El término origen de *datos* no debe confundirse con términos similares. En este manual, *DBMS* o base de *datos* hace referencia a un programa o motor de base de datos. Se hace una distinción adicional entre las bases de datos de *escritorio,* diseñadas para ejecutarse en equipos personales y a menudo carentes de soporte completo de SQL y transacciones, y bases de datos de *servidor,* diseñadas para ejecutarse en una situación cliente/servidor y caracterizadas por un motor de base de datos independiente y un rico soporte de SQL y transacciones. *Base* de datos también hace referencia a una colección determinada de datos, como una colección de archivos Xbase en un directorio o una base de datos en SQL Server. Por lo general, es equivalente al término *catálogo,* utilizado en otra parte de este manual, o al *calificador* de términos en versiones anteriores de ODBC.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de fuentes de datos](../../odbc/reference/types-of-data-sources.md)  
  
-   [Usar orígenes de datos](../../odbc/reference/using-data-sources.md)  
  
-   [Ejemplo de origen de datos](../../odbc/reference/data-source-example.md)
