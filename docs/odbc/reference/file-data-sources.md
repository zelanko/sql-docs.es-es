---
title: Fuentes de datos de archivos ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0661aa424a7a118b8b12f4bf8433987ff83bd788
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306656"
---
# <a name="file-data-sources"></a>Orígenes de datos de archivo
*Los orígenes* de datos de archivo se almacenan en un archivo y permiten que la información de conexión sea utilizada repetidamente por un solo usuario o compartida entre varios usuarios. Cuando se utiliza un origen de datos de archivo, el Administrador de controladores realiza la conexión al origen de datos mediante la información de un archivo .dsn. Este archivo se puede manipular como cualquier otro archivo. Un origen de datos de archivo no tiene un nombre de origen de datos, al igual que un origen de datos de máquina, y no está registrado en ningún usuario o equipo.  
  
 Un origen de datos de archivo simplifica el proceso de conexión, porque el archivo .dsn contiene la cadena de conexión que, de lo contrario, tendría que compilarse para una llamada a la función **SQLDriverConnect.** Otra ventaja del archivo .dsn es que se puede copiar en cualquier equipo, por lo que muchos equipos pueden utilizar orígenes de datos idénticos siempre que tengan instalado el controlador adecuado. Las aplicaciones también pueden compartir un origen de datos de archivo. Un origen de datos de archivo compartible puede colocarse en una red y utilizarse simultáneamente en varias aplicaciones.  
  
 Un archivo .dsn también puede ser no compartible. Un archivo .dsn no compartible reside en un único equipo y apunta a un origen de datos de la máquina. Los orígenes de datos de archivos no compartibles existen principalmente para permitir la fácil conversión de orígenes de datos de máquina a orígenes de datos de archivo para que una aplicación se pueda diseñar para trabajar únicamente con orígenes de datos de archivos. Cuando se envía la información en un origen de datos de archivo no compartible, se conecta según sea necesario al origen de datos del equipo al que apunta el archivo .dsn.  
  
 Para obtener más información acerca de los orígenes de datos de archivo, vea Conexión mediante [orígenes](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)de datos de archivo o la descripción de la función [SQLDriverConnect.](../../odbc/reference/syntax/sqldriverconnect-function.md)
