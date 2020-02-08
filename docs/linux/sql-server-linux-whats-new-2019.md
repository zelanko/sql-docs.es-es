---
title: Novedades de SQL Server 2019 en Linux
description: En este artículo se destacan las novedades de SQL Server 2019 en Linux.
author: VanMSFT
ms.author: vanto
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 5183efa51afd89ad82d0cdcb6448996429b81d28
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "72890560"
---
# <a name="whats-new-for-sql-server-2019-on-linux"></a>Novedades de SQL Server 2019 en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se describen las características y los servicios principales disponibles para SQL Server 2019 en ejecución en Linux. Para descargar los paquetes y consultar los problemas conocidos, vea [Notas de la versión](sql-server-linux-release-notes-2019.md?view=sql-server-linux-ver15).

## <a name="updates"></a>Actualizaciones

Las actualizaciones se han realizado en SQL Server 2019 en Linux:

| Nueva característica o actualización | Detalles |
|:-----|:-----|
|Compatibilidad con la replicación |[Replicación de SQL Server en Linux](sql-server-linux-replication.md)
|Compatibilidad con el Coordinador de transacciones distribuidas de Microsoft (MSDTC) |[Cómo configurar el Coordinador de transacciones distribuidas de Microsoft (MSDTC) en Linux](sql-server-linux-configure-msdtc.md) |
|Compatibilidad de OpenLDAP con proveedores terceros de AD |[Tutorial: Usar la autenticación de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md) |
|Machine Learning en Linux |[Instalar Machine Learning en Linux](sql-server-linux-setup-machine-learning.md) |
|Mejoras de `tempdb` | De forma predeterminada, una nueva instalación de SQL Server en Linux crea varios archivos de datos `tempdb` en función del número de núcleos lógicos (con un máximo de 8 archivos de datos). Esto no es aplicable a actualizaciones de versión principal o secundaria en contexto. Cada archivo `tempdb` es de 8 MB con un crecimiento automático de 64 MB. Este comportamiento es similar a la instalación de SQL Server predeterminada en Windows. |
| PolyBase en Linux | [Instale PolyBase](../relational-databases/polybase/polybase-linux-setup.md) en Linux para conectores que no son Hadoop.<br/><br/>[Asignación del tipo de PolyBase](../relational-databases/polybase/polybase-type-mapping.md). |
| Compatibilidad con Captura de datos modificados (CDC) | Captura de datos modificados (CDC) ahora es compatible con Linux para SQL Server 2019. |
| Registro de contenedor de Microsoft | Ahora [Registro de contenedor de Microsoft](https://www.ntweekly.com/2019/09/23/microsoft-container-registry-to-replace-docker-hub-for-new-images/) reemplaza a Docker Hub para nuevas imágenes de contenedor de Microsoft oficiales, incluido [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. |
| Contenedores no raíz | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] presenta la capacidad de crear contenedores más seguros mediante el inicio del proceso de [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] como un usuario no raíz de forma predeterminada. Vea [Compilación y ejecución de contenedores de SQL Server como un usuario no raíz](sql-server-linux-configure-docker.md#buildnonrootcontainer) para más información. |

## <a name="next-steps"></a>Pasos siguientes

Para instalar SQL Server en Linux, use uno de los siguientes tutoriales:

- [Instalación en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md?view=sql-server-linux-ver15)
- [Instalación en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md?view=sql-server-linux-ver15)
- [Instalación en Ubuntu](quickstart-install-connect-ubuntu.md?view=sql-server-linux-ver15)
- [Ejecución en Docker](quickstart-install-connect-docker.md?view=sql-server-linux-ver15)
- [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

Para obtener respuesta a las preguntas más frecuentes, vea [Preguntas más frecuentes sobre SQL Server en Linux](sql-server-linux-faq.md). Para ver otras mejoras presentadas en SQL Server 2019, vea [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
