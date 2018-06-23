---
title: Procesar resultados | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [SQL Server Native Client]
ms.assetid: 20887ac4-f649-4e7f-92e6-f929e2e70952
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7b1f2d039cf88e8487433d0d92e2e0f6c265f637
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104677"
---
# <a name="processing-results"></a>Procesar los resultados (ODBC)
  Si se crea un objeto de conjunto de filas por la ejecución de un comando o por la generación de un objeto de conjunto de filas directamente del proveedor, el consumidor necesita recuperar y tener acceso a los datos del conjunto de filas.  
  
 Los conjuntos de filas son los objetos centrales que habilitan al proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para exponer los datos en formato tabular. Conceptualmente, un conjunto de filas es un conjunto de filas en las que cada fila tiene datos de columna. Un objeto de conjunto de filas expone interfaces como **IRowset** (contiene métodos para capturar secuencialmente las filas del conjunto de filas), **IAccessor** (permite la definición de un grupo de enlaces de columna que describe el datos de manera tabulares se enlazan a variables de programa del consumidor), **IColumnsInfo** (proporciona información acerca de las columnas del conjunto de filas), y **IRowsetInfo** (proporciona información sobre el conjunto de filas).  
  
 Un consumidor puede llamar a la **IRowset:: GetData** método para recuperar una fila de datos del conjunto de filas en un búfer. Antes de **GetData** es llama, el consumidor describe el búfer mediante un conjunto de estructuras DBBINDING. Cada enlace describe cómo una columna en un conjunto de filas se almacena en un búfer del consumidor y contiene lo siguiente:  
  
-   Ordinal de la columna (o parámetro) al que se aplica el enlace.  
  
-   Información acerca de qué se enlaza (por ejemplo, valor de los datos, longitud de los datos y su estado de enlace).  
  
-   Información acerca de qué se desplaza en el búfer a cada una de estas partes.  
  
-   La longitud y el tipo de los valores de datos tal y como existen en el búfer del consumidor.  
  
 Al obtener datos, el proveedor usa información en cada enlace para determinar donde y cómo recuperar los datos del búfer del consumidor. Al establecer datos en el búfer del consumidor, el proveedor usa información en cada enlace para determinar donde y cómo devolver los datos en el búfer del consumidor.  
  
 Después de haber especifican las estructuras DBBINDING, se crea un descriptor de acceso (**IAccessor:: CreateAccessor**). Un descriptor de acceso es una colección de enlaces que se usa para obtener o establecer los datos en el búfer del consumidor.  
  
## <a name="see-also"></a>Vea también  
 [Crear una aplicación de proveedor SQL Server Native Client OLE DB](creating-a-sql-server-native-client-ole-db-provider-application.md)   
 [Temas de procedimientos de OLE DB](../native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  