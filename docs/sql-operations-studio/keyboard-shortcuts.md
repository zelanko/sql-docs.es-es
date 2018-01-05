---
title: "Crear y personalizar métodos abreviados de teclado en las operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo crear y personalizar métodos abreviados de teclado en las operaciones de SQL Studio (versión preliminar)."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a96204723bd56a63ec23841ede47b5844fbad313
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="keyboard-shortcuts-in-includename-sosincludesname-sosmd"></a>Métodos abreviados de teclado[!INCLUDE[name-sos](../includes/name-sos.md)]

Este artículo proporciona los pasos para ver, editar y crear métodos abreviados de teclado rápidamente [!INCLUDE[name-sos](../includes/name-sos-short.md)].

Dado que [!INCLUDE[name-sos](../includes/name-sos-short.md)] hereda su funcionalidad de enlace de teclado de Visual Studio Code, información detallada acerca de las personalizaciones avanzadas, con distintas distribuciones de teclado, etc., están en el [enlaces de clave para el código de Visual Studio](https://code.visualstudio.com/docs/getstarted/keybindings) artículo. Algunas características de keybinding no estén disponibles (por ejemplo, no se admiten las extensiones de mapa de teclas en [!INCLUDE[name-sos](../includes/name-sos-short.md)]).


## <a name="open-the-keyboard-shortcuts-editor"></a>Abra el editor de métodos abreviados de teclado

Para ver todos los métodos abreviados de teclado definidos actualmente:

Abra la **métodos abreviados de teclado** editor desde el **archivo** menú: **archivo** > **preferencias**  >   **Métodos abreviados de teclado** (**[!INCLUDE[name-sos](../includes/name-sos-short.md)]** > **preferencias** > **métodos abreviados de teclado** en Mac).

Además de mostrar los enlaces de teclado actual, el **métodos abreviados de teclado** editor enumera los comandos disponibles que no tienen métodos abreviados de teclado definidos. El **métodos abreviados de teclado** editor permite fácilmente cambiar, quitar, restablecer y definir los enlaces de teclado nuevo.  


## <a name="edit-existing-keyboard-shortcuts"></a>Editar métodos abreviados de teclado existentes

Para cambiar el keybinding para un método abreviado de teclado existente:

1. Busque el método abreviado de teclado que desea cambiar mediante el cuadro Buscar o desplazarse a través de la lista.
   > [!TIP]
   > Buscar por clave, comando, por código fuente, etc. para devolver todos los métodos abreviados de teclado correspondientes.

1. Haga clic en la entrada deseada y seleccione **Keybinding de cambio**

   ![editar el método abreviado de teclado](media/keyboard-shortcuts/change-keybinding.png)

1. Presione la combinación deseada de claves, a continuación, presione **ENTRAR** para guardarlo. 

   ![Guarde el método abreviado de teclado](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>Crear nuevos métodos abreviados de teclado

Para crear nuevos métodos abreviados de teclado:

1. Haga clic en un comando que no tiene ningún keybinding y seleccione **agregar Keybinding**.

   ![Crear método abreviado de teclado](media/keyboard-shortcuts/add-keybinding.png)

1. Presione la combinación deseada de claves, a continuación, presione **ENTRAR** para guardarlo.


