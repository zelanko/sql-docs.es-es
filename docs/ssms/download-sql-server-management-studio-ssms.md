---
title: Descargar SQL Server Management Studio (SSMS) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
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
ms.custom: ''
ms.date: 07/26/2019
ms.openlocfilehash: cb379078fe5d8c2436b220871d84d352a8619155
ms.sourcegitcommit: 2604e13627fbc9f3bda3926b67045fceb7b04e37
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2019
ms.locfileid: "68823121"
---
# <a name="download-sql-server-management-studio-ssms"></a>Descarga de SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SQL Server Management Studio (SSMS) es un entorno integrado para administrar cualquier infraestructura de SQL, desde SQL Server a Azure SQL Database. SSMS proporciona herramientas para configurar, supervisar y administrar instancias de SQL Server y bases de datos. Use SSMS para implementar, supervisar y actualizar los componentes de nivel de datos que usan las aplicaciones, además de compilar consultas y scripts.

Use SSMS para consultar, diseñar y administrar bases de datos y almacenes de datos, estén donde estén, en el equipo local o en la nube.

SSMS es gratuito.

## <a name="download-ssms-182"></a>Descarga de SSMS 18.2

**SSMS 18.2 ya está disponible y es la versión de disponibilidad general (GA) más reciente de *SQL Server Management Studio* que ofrece compatibilidad con [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].**

**[![descargar](../ssdt/media/download.png) Descargar SQL Server Management Studio 18.2](https://go.microsoft.com/fwlink/?linkid=2099720)**

SSMS 18.2 es la versión de disponibilidad general (GA) más reciente de SSMS. Si tiene instalada una versión anterior de disponibilidad general de SSMS 18, la instalación de SSMS 18.2 la actualiza a 18.2. Si tiene instalada una *versión preliminar* de SSMS 18 anterior, desinstálela antes de instalar SSMS 18.2.

**Información de versión**

- Número de versión: 18.2  
- Número de compilación: 15.0.18142.0  
- Fecha de publicación: 25 de julio de 2019  

Si tiene comentarios o sugerencias, o quiere informar de alguna incidencia, la mejor manera de contactar con el equipo de SSMS es a través de [UserVoice](https://aka.ms/sqlfeedback).

La instalación de SSMS 18.x no actualiza ni reemplaza las versiones 17.x de SSMS ni las anteriores. SSMS 18.x se instala en paralelo con versiones anteriores de modo que ambas versiones estén disponibles para su uso.

Si un equipo contiene instalaciones en paralelo de SSMS, compruebe si inicia la versión correcta para sus necesidades específicas. La versión más reciente tiene la etiqueta **Microsoft SQL Server Management Studio 18**

## <a name="available-languages-ssms-182"></a>Idiomas disponibles (SSMS 18.2)

Esta versión de SSMS puede instalarse en los idiomas siguientes:

SQL Server Management Studio 18.2:  
[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2099720&clcid=0x40a)

> [!NOTE]
> El módulo SQL Server PowerShell se instala de forma independiente a través de la Galería de PowerShell. Para más información, vea [Descarga del módulo de PowerShell de SQL Server](download-sql-server-ps-module.md).

## <a name="new-in-this-release-ssms-182"></a>Novedades de esta versión (SSMS 18.2)

|  Nuevo elemento  |  Detalles  |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Always Encrypted | Se ha actualizado el proveedor de enclave para admitir la atestación de Azure. |
| Intellisense/Editor | Se ha agregado compatibilidad con la clasificación de datos.  |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | Cuadro de diálogo Índice de SSMS: se ha agregado la nueva opción de índice OPTIMIZE_FOR_SEQUENTIAL_KEY. |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | Se ha agregado compatibilidad con IntelliSense. |
| Ejecución o resultados de la consulta | Se ha agregado una "hora de finalización" en los mensajes en los que se realiza el seguimiento cuando una consulta determinada ha completado su ejecución. |
| Ejecución o resultados de la consulta  | Permite que se muestren más datos (resultado a texto) y se almacenen en celdas (resultado a cuadrícula). SSMS ahora admite hasta 2 M de caracteres para ambos (hasta 256 K y 64 K, respectivamente). Esto también ha solucionado la incidencia por la que los usuarios no podían obtener más de 43 680 caracteres de las celdas de la cuadrícula. |
| ShowPlan | Se ha agregado un nuevo atributo en QueryPlan cuando la característica escalar en línea UDF está habilitada (ContainsInlineScalarTsqlUdfs). |
| SMO | Se ha agregado compatibilidad con las "Restricciones de características". Para obtener información sobre la propia característica, vea [Restricciones de características](https://docs.microsoft.com/sql/relational-databases/security/feature-restrictions). Para obtener información sobre las extensiones de valoración, consulte [Introducción a la API de SQL Assessment](https://techcommunity.microsoft.com/t5/SQL-Server/Introducing-SQL-Assessment-API-Public-Preview/ba-p/778570). |
| Integration Services (SSIS) | Optimización del rendimiento del programador de paquetes SSIS en Azure. |
|  |  |

Para más detalles sobre las novedades de esta versión, consulte las [notas de la versión de SSMS](release-notes-ssms.md).

## <a name="supported-sql-offerings-ssms-182"></a>Ofertas de SQL admitidas (SSMS 18.2)

* Esta versión de SSMS funciona con todas las [versiones compatibles de SQL Server 2008 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) y proporciona el mayor nivel de compatibilidad para trabajar con las últimas características de nube en Azure SQL Database y en Azure SQL Data Warehouse.
* Además, SSMS 18.x puede instalarse en paralelo con SSMS 17.x, SSMS 16.x o SQL Server 2014 SSMS y versiones anteriores.
* SQL Server Integration Services (SSIS): SSMS versión 17.x o versiones posteriores no admite la conexión con el servicio heredado de SQL Server Integration Services. Para conectarse a una versión anterior del servicio heredado de Integration Services, use la versión de SSMS alineada con la versión de SQL Server. Por ejemplo, use SSMS 16.x para conectar con el servicio heredado de SQL Server 2016 Integration Services. SSMS 17.x y SSMS 16.x pueden instalarse en paralelo en el mismo equipo. Desde el lanzamiento de SQL Server 2012, la base de datos del catálogo de SSIS (SSISDB) es la manera recomendada de almacenar, administrar, ejecutar y supervisar los paquetes de Integration Services. Para más información, vea [Catálogo de SSIS](../integration-services/catalog/ssis-catalog.md).

## <a name="supported-operating-systems-ssms-182"></a>Sistemas operativos admitidos (SSMS 18.2)

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
> SSMS se ejecuta solamente en Windows. Si necesita una herramienta que se ejecuta en plataformas distintas de Windows, eche un vistazo a Azure Data Studio. Azure Data Studio es una nueva herramienta multiplataforma que se ejecuta en macOS, Linux y Windows. Para más detalles, vea [What is Azure Data Studio?](../azure-data-studio/what-is.md) ¿Qué es Azure Data Studio?.

## <a name="release-notes-ssms-182"></a>Notas de la versión (SSMS 18.2)

Hay algunos [problemas conocidos](release-notes-ssms.md#known-issues-181) con esta versión.

Para más detalles sobre esta versión, vea las [notas de la versión de SSMS](release-notes-ssms.md).

## <a name="previous-ssms-releases"></a>Versiones de SSMS anteriores

[Versiones anteriores de SQL Server Management Studio](../ssms/release-notes-ssms.md#previous-ssms-releases)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## <a name="see-also"></a>Vea también

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Documentación de SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Service Pack y actualizaciones adicionales](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [Descargar SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
