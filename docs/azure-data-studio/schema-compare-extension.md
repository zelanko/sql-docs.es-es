---
title: Extensión Schema Compare
description: Obtenga información sobre cómo instalar y usar la extensión Comparación de esquemas de Azure Data Studio para comparar fácilmente dos bases de datos y cambiar una de forma selectiva para que coincida con la otra.
ms.custom: seodec18
ms.date: 11/04/2019
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 80aa0be8ae70773fe0e1a0087e623f679504a983
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411231"
---
# <a name="schema-compare-extension"></a>Extensión Schema Compare
La extensión Comparación de esquemas proporciona una experiencia fácil de usar para comparar dos definiciones de bases de datos y aplicar las diferencias del origen al destino.


## <a name="features"></a>Características

* Comparar esquemas de dos archivos o bases de datos dacpac.
* Ver los resultados como un conjunto de acciones que deben tomarse en el destino para que coincida con el origen.
* Excluir selectivamente las acciones enumeradas en los resultados.
* Establecer las opciones que controlan el ámbito de la comparación.
* Aplicar los cambios al destino o generar un script con el mismo efecto.
* Guardar la comparación.

![Comparación de esquemas: Comparación de ejemplo](media/extensions/schema-compare-extension/schema-compare.png)


## <a name="why-would-i-use-the-schema-compare-extension"></a>¿Por qué debo usar la extensión Comparación de esquemas?

Puede resultar tedioso administrar y sincronizar manualmente versiones distintas de base de datos. La extensión Comparación de esquemas simplifica el proceso de comparación de las bases de datos y proporciona control total al sincronizarlas &mdash; puede filtrar selectivamente las diferencias y categorías de diferencias concretas antes de aplicar los cambios. La extensión Comparación de esquemas es una herramienta de confianza que le permitirá ahorrar tiempo y código.

![Comparación de esquemas: Cuadro de diálogo Opciones](media/extensions/schema-compare-extension/schema-compare-options.png)


## <a name="install-the-extension"></a>Instalación de la extensión

1. Seleccione el icono de extensiones para ver las extensiones disponibles.

    ![Icono del Administrador de extensiones](media/extensions/extension-manager-icon.png)

2. Busque la extensión **Comparación de esquemas** y selecciónela para ver los detalles. Haga clic en **Instalar** para agregar la extensión.

3. Una vez instalada, seleccione **Recargar** para habilitar la extensión en Azure Data Studio (solo es necesario cuando se instala una extensión por primera vez).


## <a name="launch-a-schema-compare"></a>Inicio de una Comparación de esquemas

1. Para abrir el cuadro de diálogo de Comparación de esquemas, **haga clic con el botón derecho** en una base de datos en el Explorador de objetos y luego en **Comparación de esquemas**. La base de datos seleccionada se establecerá como la base de datos de origen en la comparación.

    ![menú de inicio de la Comparación de esquemas](media/extensions/schema-compare-extension/schema-compare-launch.png)


2. Seleccione uno de los puntos suspensivos (...) para cambiar el origen y el destino de la Comparación de esquemas y haga clic en Aceptar.

    ![selección de origen y destino de la Comparación de esquemas](media/extensions/schema-compare-extension/schema-compare-select-source-target.png)

3. Para personalizar la comparación, haga clic en el botón **Opciones** de la barra de herramientas.

4. Haga clic en **Comparar** para ver los resultados de la comparación.


## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la comparación de esquemas, consulte [nuestra documentación](https://docs.microsoft.com/sql/ssdt/how-to-use-schema-compare-to-compare-different-database-definitions).
Puede notificar cualquier problema y solicitar nuevas características [aquí](https://github.com/microsoft/azuredatastudio/issues).