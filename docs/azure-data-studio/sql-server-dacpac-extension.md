---
title: Extensión dacpac de SQL Server
description: Aprenda a instalar e iniciar el Asistente para aplicaciones de capa de datos, que facilita la implementación y extracción de archivos dacpac y la importación y exportación de archivos bacpac.
ms.custom: seodec18
ms.date: 11/04/2019
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 709e218727ad85fdf220033e3d8ea8741451fd9e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766014"
---
# <a name="sql-server-dacpac-extension"></a>Extensión dacpac de SQL Server

El **Asistente para aplicaciones de capa de datos** proporciona una experiencia de asistente fácil de usar para implementar y extraer archivos dacpac, así como para importar y exportar archivos bacpac.


## <a name="features"></a>Características

* Implementación de un archivo dacpac en una instancia de SQL Server
* Extracción de una instancia de SQL Server en un archivo dacpac
* Creación de una base de datos a partir de un archivo bacpac
* Exportación del esquema y los datos a un archivo bacpac

![GIF de demostración de la extensión del archivo dacpac](media/extensions/sql-server-dacpac-extension/dacpac-extension-demo.gif)


## <a name="why-would-i-use-the-data-tier-application-wizard"></a>¿Por qué es tan útil Asistente para aplicaciones de capa de datos?

El asistente facilita la administración de archivos dacpac y bacpac, lo que simplifica el desarrollo y la implementación de los elementos de capa de datos que admiten la aplicación. Para obtener más información sobre el uso de las aplicaciones de capa de datos, [vea nuestra documentación.](../relational-databases/data-tier-applications/data-tier-applications.md?view=sql-server-2017)


## <a name="install-the-extension"></a>Instalación de la extensión

1. Seleccione el icono de extensiones para ver las extensiones disponibles.

    ![Icono del Administrador de extensiones](media/extensions/extension-manager-icon.png)

2. Busque la extensión **SQL Server dacpac** y selecciónela para ver los detalles. Haga clic en **Instalar** para agregar la extensión.

3. Una vez instalada, seleccione **Recargar** para habilitar la extensión en Azure Data Studio (solo es necesario cuando se instala una extensión por primera vez).


## <a name="launch-the-data-tier-application-wizard"></a>Inicio del asistente de aplicaciones de capa de datos

Para iniciar el asistente, haga clic con el botón secundario en la carpeta Databases o haga clic con el botón secundario en una base de datos específica en el Explorador de objetos. A continuación, haga clic en **Asistente para aplicaciones de capa de datos**.

![menú de inicio de la extensión dacpac](media/extensions/sql-server-dacpac-extension/dacpac-extension-launch.png)


## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre dacpac, [vea nuestra documentación](../relational-databases/data-tier-applications/data-tier-applications.md?view=sql-server-2017).
Puede notificar cualquier problema y solicitar nuevas características [aquí](https://github.com/microsoft/azuredatastudio/issues).