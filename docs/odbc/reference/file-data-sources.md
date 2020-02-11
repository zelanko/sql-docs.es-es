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
ms.openlocfilehash: 9d27f168640b25652ed0fd40154ebfb677ef9300
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068645"
---
# <a name="file-data-sources"></a>Orígenes de datos de archivo
Los *orígenes de datos de archivo* se almacenan en un archivo y permiten que un solo usuario pueda usar la información de conexión de forma repetida o compartida entre varios usuarios. Cuando se utiliza un origen de datos de archivo, el administrador de controladores realiza la conexión al origen de datos utilizando la información de un archivo. DSN. Este archivo se puede manipular como cualquier otro archivo. Un origen de datos de archivo no tiene un nombre de origen de datos, como un origen de datos de la máquina, y no está registrado en ningún usuario o equipo.  
  
 Un origen de datos de archivo simplifica el proceso de conexión, ya que el archivo. DSN contiene la cadena de conexión que, de lo contrario, tendría que compilarse para una llamada a la función **SQLDriverConnect** . Otra ventaja del archivo. DSN es que se puede copiar en cualquier equipo, por lo que muchos equipos pueden usar orígenes de datos idénticos siempre que tengan instalado el controlador adecuado. Las aplicaciones también pueden compartir un origen de datos de archivo. Un origen de datos de archivo que se puede compartir puede colocarse en una red y usarse simultáneamente en varias aplicaciones.  
  
 Un archivo. DSN también puede ser no compartible. Un archivo. DSN que no se pueda compartir reside en un solo equipo y apunta a un origen de datos de la máquina. Los orígenes de datos de archivos que no se pueden compartir existen principalmente para permitir la conversión sencilla de orígenes de datos de equipo en orígenes de datos de archivo, de modo que una aplicación pueda diseñarse para funcionar exclusivamente con orígenes de datos de archivo. Cuando el administrador de controladores envía la información de un origen de datos de archivos que no se pueden compartir, se conecta según sea necesario en el origen de datos de la máquina al que apunta el archivo. DSN.  
  
 Para obtener más información acerca de los orígenes de datos de archivo, vea [conectarse con orígenes de datos de archivo](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)o la descripción de la función [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) .
