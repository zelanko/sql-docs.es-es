---
title: Orígenes de datos de archivo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 733b958ee883aa62034b4acc1eec67100b35a74d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809273"
---
# <a name="file-data-sources"></a>Orígenes de datos de archivo
*Orígenes de datos de archivo* se almacenan en un archivo y permitir que se usan repetidamente un único usuario o compartir entre varios usuarios la información de conexión. Cuando se usa un origen de datos de archivo, el Administrador de controladores hace que la conexión al origen de datos con la información de un archivo DSN. Este archivo se puede manipular como cualquier otro archivo. Un origen de datos de archivo no tiene un nombre de origen de datos, como hace un origen de datos de la máquina y no está registrado en cualquier máquina o un usuario.  
  
 Un origen de datos de archivos simplifica el proceso de conexión, porque el archivo .dsn contiene la cadena de conexión que tendría que compilarse para llamar a la **SQLDriverConnect** función. Otra ventaja del archivo DSN es que puede copiar cualquier máquina, por lo que los orígenes de datos idénticos pueden utilizarse por muchos equipos, siempre y cuando tengan que el controlador apropiado instalado. Las aplicaciones también puede compartir un origen de datos de archivo. Un origen de datos que se pueda compartir archivo se puede colocar en una red y utilizar simultáneamente varias aplicaciones.  
  
 También se pueden compartir un archivo DSN. Un archivo DSN no se puede compartir reside en un único equipo y apunta a un origen de datos de la máquina. Orígenes de datos de archivo no se puede compartir existen principalmente para permitir la conversión sencilla de orígenes de datos de la máquina a orígenes de datos de archivo para que una aplicación puede diseñarse para trabajar exclusivamente con orígenes de datos de archivo. Cuando el Administrador de controladores se envía la información en un origen de datos no se puede compartir archivos, se conecta según sea necesario para el origen de datos de la máquina que apunta el archivo DSN.  
  
 Para obtener más información acerca de los orígenes de datos de archivo, consulte [conecta orígenes de datos de archivo utilizando](../../odbc/reference/develop-app/connecting-using-file-data-sources.md), o el [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) descripción de la función.
