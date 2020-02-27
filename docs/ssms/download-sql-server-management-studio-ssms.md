---
title: Descarga de SQL Server Management Studio (SSMS)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
keywords:
- instalar ssms, descargar ssms, versiones de ssms más recientes
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- instalación de sql management studio
- descargar sql management studio
- ms sql management studio
- instalar sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
author: dnethi
ms.author: dinethi
ms.reviewer: sstein, maghan
ms.custom: seo-lt-2019
ms.date: 02/18/2020
ms.openlocfilehash: 5004b46f878a5098e63fb3842569e826b21b764f
ms.sourcegitcommit: 5a9b8bc4fcb5e875d5ef25362b68ffe7f8a1b6d7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/21/2020
ms.locfileid: "77520948"
---
# <a name="download-sql-server-management-studio-ssms"></a>Descarga de SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SQL Server Management Studio (SSMS) es un entorno integrado para administrar cualquier infraestructura de SQL, desde SQL Server a Azure SQL Database. SSMS proporciona herramientas para configurar, supervisar y administrar instancias de SQL Server y bases de datos. Use SSMS para implementar, supervisar y actualizar los componentes de nivel de datos que usan las aplicaciones, además de compilar consultas y scripts.

Use SSMS para consultar, diseñar y administrar bases de datos y almacenes de datos, estén donde estén, en el equipo local o en la nube.

SSMS es gratuito.

## <a name="download-ssms"></a>Descargar SSMS

**[![descargar](media/download-icon.png) Descarga de SQL Server Management Studio (SSMS)](https://aka.ms/ssmsfullsetup)**

SSMS 18.4 es la versión de disponibilidad general más reciente de SSMS. Si tiene instalada una versión anterior de disponibilidad general de SSMS 18, esta se actualizará a 18.4 con la nueva instalación.

### <a name="version-information"></a>Información de la versión

- Número de versión: 18.4  
- Número de compilación: 15.0.18206.0  
- Fecha de lanzamiento: 4 de noviembre de 2019  

Si tiene comentarios o sugerencias, o quiere informar de alguna incidencia, la mejor manera de contactar con el equipo de SSMS es a través de [UserVoice](https://aka.ms/sqlfeedback).

La instalación de SSMS 18.x no actualiza ni reemplaza las versiones 17.x de SSMS ni las anteriores. SSMS 18.x se instala en paralelo con versiones anteriores de modo que ambas versiones estén disponibles para su uso. Sin embargo, si tiene instalada una ***versión preliminar*** de SSMS 18.x, debe **desinstalarla** antes de instalar SSMS 18.4. Para ver si tiene la *versión preliminar*, vaya a la ventana Ayuda > Acerca de.

Si un equipo contiene instalaciones en paralelo de SSMS, compruebe si inicia la versión correcta para sus necesidades específicas. La versión más reciente tiene la etiqueta **Microsoft SQL Server Management Studio 18**

> [!Note]
> Si accede a esta página desde una versión de idioma que no es el inglés y quiere ver el contenido más actualizado, visite la [versión en inglés de EE. UU. del sitio](https://aka.ms/downloadssmsusenglish). Puede descargar distintos idiomas en el sitio de la versión en inglés de EE. UU. si selecciona [idiomas disponibles](#available-languages).

## <a name="available-languages"></a>Idiomas disponibles

Esta versión de SSMS puede instalarse en los idiomas siguientes:

SQL Server Management Studio 18.4:  
[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2108895&clcid=0x40a)

> [!NOTE]
> El módulo SQL Server PowerShell se instala de forma independiente a través de la Galería de PowerShell. Para más información, vea [Descarga del módulo de PowerShell de SQL Server](download-sql-server-ps-module.md).

## <a name="whats-new"></a>Novedades

Para obtener más detalles e información sobre las novedades de esta versión, vea [Notas de la versión de SSMS](release-notes-ssms.md).

Hay algunos [problemas conocidos](release-notes-ssms.md#known-issues-184) con esta versión.

## <a name="previous-versions"></a>Versiones anteriores

Este artículo es exclusivo para la versión más reciente de SSMS. Para descargar versiones anteriores de SSMS, visite [Versiones anteriores de SSMS](../ssms/release-notes-ssms.md#previous-ssms-releases).

## <a name="supported-sql-offerings-ssms-184"></a>Ofertas de SQL admitidas (SSMS 18.4)

- Esta versión de SSMS funciona con todas las [versiones compatibles de SQL Server 2008 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) y proporciona el mayor nivel de compatibilidad para trabajar con las últimas características de nube en Azure SQL Database y en Azure SQL Data Warehouse.
- Además, SSMS 18.x puede instalarse en paralelo con SSMS 17.x, SSMS 16.x o SQL Server 2014 SSMS y versiones anteriores.
- SQL Server Integration Services (SSIS): SSMS versión 17.x o versiones posteriores no admite la conexión con el servicio heredado de SQL Server Integration Services. Para conectarse a una versión anterior del servicio heredado de Integration Services, use la versión de SSMS alineada con la versión de SQL Server. Por ejemplo, use SSMS 16.x para conectar con el servicio heredado de SQL Server 2016 Integration Services. SSMS 17.x y SSMS 16.x pueden instalarse en paralelo en el mismo equipo. Desde el lanzamiento de SQL Server 2012, la base de datos del catálogo de SSIS (SSISDB) es la manera recomendada de almacenar, administrar, ejecutar y supervisar los paquetes de Integration Services. Para más información, vea [Catálogo de SSIS](../integration-services/catalog/ssis-catalog.md).

## <a name="supported-operating-systems-ssms-184"></a>Sistemas operativos admitidos (SSMS 18.4)

Esta versión de SSMS admite las siguientes plataformas de 64 bits cuando se usa con el Service Pack más reciente disponible:

- Windows 10 (64 bits) <sup>*</sup>
- Windows 8.1 (64 bits)
- Windows Server 2019 (64 bits)
- Windows Server 2016 (64 bits) <sup>*</sup>
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

<sup>*</sup> Necesita la versión 1607 (10.0.14393) o posterior

> [!NOTE]
> SSMS solo se ejecuta en Windows (AMD o Intel). Si necesita una herramienta que se ejecuta en plataformas distintas de Windows, eche un vistazo a Azure Data Studio. Azure Data Studio es una nueva herramienta multiplataforma que se ejecuta en macOS, Linux y Windows. Para más detalles, vea [What is Azure Data Studio?](../azure-data-studio/what-is.md) ¿Qué es Azure Data Studio?.

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## <a name="see-also"></a>Consulte también

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Documentación de SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Actualizaciones más recientes](../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)
- [Descargar las últimas herramientas de datos SQL Server](../ssdt/download-sql-server-data-tools-ssdt.md)
- [Guía de arquitectura de datos de Azure](https://docs.microsoft.com/azure/architecture/data-guide/)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
