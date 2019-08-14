---
title: Extensión Schema Compare
titleSuffix: Azure Data Studio
description: Instalación y uso de la extensión Schema Compare (versión preliminar) para Azure Data Studio
ms.custom: seodec18
ms.date: 06/06/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: a51d64202d3d906b3106092084628b0a961297ea
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959326"
---
# <a name="schema-compare-extension-preview"></a>Extensión Comparación de esquemas (versión preliminar)
La extensión Schema Compare proporciona una experiencia fácil de usar para comparar bases de datos y archivos .dacpac y aplicar los cambios del origen al destino.

Esta experiencia está actualmente en su versión preliminar inicial. Puede notificar cualquier problema y solicitar nuevas características [aquí](https://github.com/microsoft/azuredatastudio/issues).

## <a name="install-the-schema-compare-extension"></a>Instalación de la extensión Schema Compare

1. Para abrir el administrador de extensiones y acceder a las extensiones disponibles, seleccione el icono de extensiones o bien elija **Extensiones** en el menú **Ver**.
2. Seleccione una extensión disponible para ver sus detalles.
1. Seleccione la extensión que quiere (Schema Compare) e **instálela**.

## <a name="how-do-i-start-a-schema-comparison"></a>¿Cómo se inicia una comparación de esquemas?
* El punto de entrada principal del asistente consiste en hacer clic con el botón derecho en una base de datos en el Explorador de objetos y luego hacer clic en **Comparación de esquemas**.
* El usuario también puede iniciar el cuadro de diálogo Comparación de esquemas desde la paleta de comandos (Ctrl+Mayús+P) buscando **Comparación de esquemas**

## <a name="why-would-i-use-the-schema-compare"></a>¿Por qué debo usar la comparación de esquemas?
La comparación de esquemas se creó para agregar la posibilidad de comparar los esquemas de las bases de datos y los archivos .dacpac y aplicar los cambios.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre la comparación de esquemas, consulte [nuestra documentación](https://docs.microsoft.com/sql/ssdt/how-to-use-schema-compare-to-compare-different-database-definitions).


