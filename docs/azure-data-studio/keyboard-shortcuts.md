---
title: Creación y personalización de métodos abreviados de teclado
titleSuffix: Azure Data Studio
description: Aprenda a crear y personalizar métodos abreviados de teclado en Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 8e577f50152eb5f86b81caa23cc493b92bbab270
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67959473"
---
# <a name="keyboard-shortcuts-in-includename-sosincludesname-sosmd"></a>Accesos directos del teclado en [!INCLUDE[name-sos](../includes/name-sos.md)]

En este artículo se proporcionan los pasos para ver, editar y crear rápidamente métodos abreviados de teclado en [!INCLUDE[name-sos](../includes/name-sos-short.md)].

Dado que [!INCLUDE[name-sos](../includes/name-sos-short.md)] hereda su funcionalidad de enlace de teclado de Visual Studio Code, la información detallada sobre las personalizaciones avanzadas, el uso de diferentes distribuciones de teclado, etc., se encuentra en el artículo sobre los [enlaces de teclado de Visual Studio Code](https://code.visualstudio.com/docs/getstarted/keybindings). Es posible que algunas características de enlace de teclado no estén disponibles (por ejemplo, las extensiones de distribución de teclado no se admiten en [!INCLUDE[name-sos](../includes/name-sos-short.md)]).


## <a name="open-the-keyboard-shortcuts-editor"></a>Abra el editor de métodos abreviados de teclado

Para ver todos los métodos abreviados de teclado actualmente definidos:

Abra el editor de **métodos abreviados de teclado** desde el menú **Archivo**: **Archivo** > **Preferencias** > **Métodos abreviados de teclado** ( **[!INCLUDE[name-sos](../includes/name-sos-short.md)]**  > **Preferencias** > **Métodos abreviados de teclado** en Mac).

Además de mostrar los enlaces de teclado actuales, el editor de **métodos abreviados de teclado** enumera los comandos disponibles que no tienen definido un método abreviado de teclado. El editor de **métodos abreviados de teclado** permite cambiar, quitar, restablecer y definir fácilmente nuevos enlaces de teclado.  


## <a name="edit-existing-keyboard-shortcuts"></a>Edición de los métodos abreviados de teclado existentes

Para cambiar el enlace de teclado de un método abreviado de teclado existente:

1. Busque el método abreviado de teclado que quiera cambiar con el cuadro de búsqueda o desplazándose por la lista.
   > [!TIP]
   > Busque por clave, comando, por origen, etc. para devolver todos los métodos abreviados de teclado pertinentes.

1. Haga clic con el botón derecho en la entrada deseada y seleccione **Change Key binding** (Cambiar enlace de teclado).

   ![editar método abreviado de teclado](media/keyboard-shortcuts/change-keybinding.png)

1. Presione la combinación de teclas deseada y, después, presione **Entrar** para guardarla. 

   ![guardar método abreviado de teclado](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>Creación de nuevos métodos abreviados de teclado

Para crear nuevos métodos abreviados de teclado:

1. Haga clic con el botón derecho en un comando que no tenga ningún enlace de teclado y seleccione **Add Key binding** (Agregar enlace de teclado).

   ![crear método abreviado de teclado](media/keyboard-shortcuts/add-keybinding.png)

1. Presione la combinación de teclas deseada y, después, presione **Entrar** para guardarla.


