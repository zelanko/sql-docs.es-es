---
title: Implementación de una base de datos de Azure SQL a través de Notebook
description: En este tutorial se muestra cómo crear una base de datos de Azure SQL.
author: ninarn
ms.author: ninarn
ms.reviewer: alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 88bb9fd980da21b20f0faf6f699147d26abe65b9
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2020
ms.locfileid: "92060920"
---
# <a name="create-an-azure-sql-database-using-azure-data-studio"></a>Creación de una base de datos de Azure SQL mediante Azure Data Studio

Puede crear una base de datos de Azure SQL mediante Azure Data Studio y el Asistente para la implementación y los notebooks.

## <a name="pre-requisites"></a>Requisitos previos

 - [Azure Data Studio](download-azure-data-studio.md) instalado.
 - Una cuenta y una suscripción activas de Azure. En caso de no tener ninguna, [cree una cuenta gratuita](https://azure.microsoft.com/free/).

## <a name="use-the-deployment-wizard"></a>Usar el Asistente para la implementación

Siga estos pasos para usar el Asistente para la implementación, que le guiará a través de la configuración necesaria en una experiencia de interfaz de usuario simple.

En primer lugar, busque y seleccione Azure SQL Database en el Asistente para la implementación.

 1. En Azure Data Studio, seleccione el viewlet Conexiones en el panel de navegación izquierdo.
 2. Seleccione el botón **...** en la parte superior del panel Conexiones y elija **Nueva implementación**.
 3. En el Asistente para la implementación, seleccione el icono de **Azure SQL Database** y active la casilla de aceptación de términos.
 4. En la lista desplegable Tipo de recurso, seleccione lo que quiere crear: una base de datos, un servidor de base de datos o un grupo elástico. Si no tiene ninguna base de datos SQL en Azure, se recomienda empezar por la creación de una base de datos.
 5. Seleccione **Crear en Azure Portal**.

Después, escriba la configuración preferida para crear la base de datos, el servidor o el grupo. Puede encontrar algunas instrucciones sobre cómo configurar estas opciones en la [documentación de Azure SQL](https://docs.microsoft.com/azure/azure-sql/database/single-database-create-quickstart?tabs=azure-portal).

## <a name="next-steps"></a>Pasos siguientes

Después de crear la base de datos, el servidor o el grupo, puede [conectarse y consultar](quickstart-sql-database.md) la base de datos en Azure Data Studio.
