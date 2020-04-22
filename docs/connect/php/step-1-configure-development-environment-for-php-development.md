---
title: 'Paso 1: Configuración del entorno para PHP'
description: El paso 1 de esta guía de introducción implica la instalación de PHP, Microsoft ODBC Driver for SQL Server y la configuración del entorno de desarrollo.
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0bce6022-00bd-45c6-9671-eaa9dfa395a8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88eb2c2c67eac3ecd9fba2c79c143de28cf60d22
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/17/2020
ms.locfileid: "81633176"
---
# <a name="step-1-configure-environment-for-php-development"></a>Paso 1: Configuración del entorno para el desarrollo en PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]




* Identifique qué versión del controlador PHP va a usar en función de su entorno, como se indica aquí:  [Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server](system-requirements-for-the-php-sql-driver.md)
* Descargue e instale el controlador PHP aplicable aquí: [Descargar controladores de Microsoft para PHP](https://www.microsoft.com/download/details.aspx?id=20098)  
* Descargue e instale el controlador ODBC aplicable aquí:  [Descargar controlador ODBC para SQL Server](../odbc/download-odbc-driver-for-sql-server.md)  
* Configure el controlador PHP y el servidor web para su sistema operativo específico:

### <a name="windows"></a>Windows  
  

* Configure la carga del controlador PHP, como se indica aquí: [Carga de los controladores de Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md) 
* Configure IIS para hospedar aplicaciones PHP, como se indica aquí: [Configuración de IIS para los controladores de Microsoft para PHP para SQL Server](../../connect/php/configuring-iis-for-php-sql-driver.md)

### <a name="linux-and-macos"></a>Linux y macOS


*   Configure la carga del controlador PHP y configure el servidor web para hospedar aplicaciones PHP, como se indica aquí: [Tutorial de instalación de controladores PHP en Linux y macOS](../../connect/php/installation-tutorial-linux-mac.md)
