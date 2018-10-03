---
title: Crear y personalizar métodos abreviados de teclado en Azure Data Studio | Microsoft Docs
description: Obtenga información sobre cómo crear y personalizar métodos abreviados de teclado en Azure Data Studio.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6c6fb8d7e59441af00d3741ebc53756525d1cf3e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "48039067"
---
# <a name="keyboard-shortcuts-in-includename-sosincludesname-sosmd"></a>Métodos abreviados de teclado [!INCLUDE[name-sos](../includes/name-sos.md)]

En este artículo se proporciona los pasos para ver, editar y crear métodos abreviados de teclado rápidamente [!INCLUDE[name-sos](../includes/name-sos-short.md)].

Dado que [!INCLUDE[name-sos](../includes/name-sos-short.md)] hereda su funcionalidad de enlace de teclado de Visual Studio Code, información detallada acerca de las personalizaciones avanzadas, con distintas distribuciones de teclado, etc., que está en el [enlaces de teclado para Visual Studio Code](https://code.visualstudio.com/docs/getstarted/keybindings) artículo. Algunas características de enlace de teclado no estén disponibles (por ejemplo, las extensiones de mapa de teclas no se admiten en [!INCLUDE[name-sos](../includes/name-sos-short.md)]).


## <a name="open-the-keyboard-shortcuts-editor"></a>Abra el editor de métodos abreviados de teclado

Para ver todos los métodos abreviados de teclado actualmente definidas:

Abra el **métodos abreviados de teclado** editor desde la **archivo** menú: **archivo** > **preferencias**  >   **Métodos abreviados de teclado** (**[!INCLUDE[name-sos](../includes/name-sos-short.md)]** > **preferencias** > **métodos abreviados de teclado** en Mac).

Además de mostrar los enlaces de teclado actual, el **métodos abreviados de teclado** editor enumera los comandos disponibles que no tienen métodos abreviados de teclado definidos. El **métodos abreviados de teclado** editor le permite fácilmente cambiar, quitar, restablecer y definir los enlaces de teclado nuevo.  


## <a name="edit-existing-keyboard-shortcuts"></a>Editar accesos directos de teclado existentes

Para cambiar el enlace de teclado para un método abreviado de teclado existente:

1. Busque el método abreviado de teclado que desea cambiar mediante el cuadro de búsqueda o desplazarse a través de la lista.
   > [!TIP]
   > Buscar por clave, el comando, por origen, etc. para devolver todos los métodos abreviados de teclado correspondiente.

1. Haga clic en la entrada deseada y seleccione **Keybinding de cambio**

   ![editar el método abreviado de teclado](media/keyboard-shortcuts/change-keybinding.png)

1. Presione la combinación deseada de claves, a continuación, presione **ENTRAR** para guardarlo. 

   ![Guarde el método abreviado de teclado](media/keyboard-shortcuts/save-keybinding.png)

## <a name="create-new-keyboard-shortcuts"></a>Crear nuevos métodos abreviados de teclado

Para crear nuevos métodos abreviados de teclado:

1. Haga clic en un comando que no hay ningún enlace de teclado y seleccione **agregar Keybinding**.

   ![Crear método abreviado de teclado](media/keyboard-shortcuts/add-keybinding.png)

1. Presione la combinación deseada de claves, a continuación, presione **ENTRAR** para guardarlo.


