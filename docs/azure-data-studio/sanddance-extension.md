---
title: SandDance para datos de Azure Studio
titleSuffix: Azure Data Studio
description: Uso de SandDance en Azure Data Studio
ms.custom: seodec18
ms.date: 04/18/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 683aea4066c0b27db295cc07db31ecd07fb33245
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798075"
---
# <a name="sanddance-for-azure-data-studio-preview"></a>SandDance para datos de Azure Studio (versión preliminar)
Azure Data Studio ahora ofrece una manera para crear visualizaciones rápidas para los archivos CSV y TSV que está trabajando. Esto incluye archivos locales o archivos en HDFS en el clúster grande de datos de SQL Server 2019. Esta extensión es útil al tratar de tener una rápida mirar los datos y comprender lo que está ocurriendo. Se usa una tecnología denominada SandDance desde Microsoft Research, que puede generar visualizaciones en lugar de los datos.

![animación de sanddance](https://user-images.githubusercontent.com/11507384/54236654-52d42800-44d1-11e9-859e-6c5d297a46d2.gif)

Mediante el uso de vistas fácil de entender, Ayuda de SandDance encontrar información detallada sobre los datos, lo que en la ayuda a su vez contar historias con datos, crear casos según la evidencia, pruebas de hipótesis, profundizar en la superficies explicaciones, apoyar las decisiones de las compras, o relacionar los datos en un contexto más amplio de mundo real.

SandDance usa las visualizaciones de la unidad, que se aplican a una asignación unívoca entre las filas de la base de datos y las marcas en la pantalla.
Transiciones animadas entre vistas le ayudan a mantener el contexto al interactuar con los datos.

## <a name="usage"></a>Uso

Iniciar desde el menú archivo, utilice Abrir carpeta o [Ctrl + K, Ctrl + O] para abrir el directorio que contiene el. Archivo CSV.  A continuación, desde dentro del panel Explorador, haga doble clic en el archivo .csv o .tsv y elija *vista en SandDance*.

Haga doble clic en un archivo .csv o .tsv en HDFS si te conectas a clúster grande de datos de SQL Server de 2019 y elija *vista en SandDance*.

## <a name="known-issues"></a>Problemas conocidos

Actualmente los datos deben tener la primera columna como un identificador único.

Actualmente no se limitar el número de filas que se visualiza. Sin embargo, el consumo de memoria aumenta proporcionalmente al número de filas, por lo que recomendamos que el conjunto de datos o la vista se limita a alrededor de 100 filas k.

Consulte [problemas conocidos](https://microsoft.github.io/SandDance/#known-issues)

## <a name="release-notes"></a>Notas de la versión

### <a name="100"></a>1.0.0

Versión inicial de azdata sanddance

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, [visite el repositorio de GitHub.](https://github.com/Microsoft/SandDance)
