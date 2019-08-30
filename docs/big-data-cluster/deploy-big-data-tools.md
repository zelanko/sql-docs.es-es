---
title: Instalación de herramientas de macrodatos
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo instalar las herramientas [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] usadas con (versión preliminar).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 84c7181bfd7c0ee014b382052bb6493d68251331
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153610"
---
# <a name="install-sql-server-2019-big-data-tools"></a>Instalación de las herramientas de macrodatos de SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describen las herramientas de cliente que se deben instalar para crear, administrar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] y usar (versión preliminar). En la siguiente sección se proporciona una lista de herramientas y vínculos a instrucciones de instalación. Antes de implementar un clúster de macrodatos, configure las herramientas marcadas como obligatorias en Windows o Linux.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>Herramientas de clúster de macrodatos

En la tabla siguiente se indican herramientas comunes de clúster de macrodatos y cómo instalarlas:

| Herramienta | Obligatorio | Descripción | Instalación |
|---|---|---|---|
| **python** | Sí | Python es un lenguaje de programación de alto nivel, interpretado y orientado a objetos con semántica dinámica. Muchas partes de los clústeres de macrodatos para SQL Server usan Python. | [Instalación de Python](#python)|
| **azdata** | Sí | Herramienta de línea de comandos para instalar y administrar un clúster de macrodatos. | [Instalar](deploy-install-azdata.md) |
| **kubectl**<sup>1</sup> | Sí | Herramienta de línea de comandos para supervisar el clúster de Kubernetes subyacente ([Más información](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio-SQL Server candidato de versión comercial 2019 (RC)** | Sí | Herramienta gráfica multiplataforma para consultar SQL Server. | [Instalar](#download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc) |
| **Extensión SQL Server 2019** | Sí | Extensión para Azure Data Studio que admite la conexión al clúster de macrodatos. Además proporciona un asistente para la virtualización de datos. | [Instalar](../azure-data-studio/sql-server-2019-extension.md) |
| **CLI de Azure**<sup>2</sup> | Para AKS | Interfaz de línea de comandos moderna para administrar servicios de Azure. Se usa con implementaciones de clústeres de macrodatos de AKS ([Más información](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [Instalar](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | Opcional | Interfaz de línea de comandos moderna para consultar SQL Server ([Más información](https://github.com/dbcli/mssql-cli/blob/master/README.rst)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | Para algunos scripts | Herramienta de línea de comandos heredada para consultar SQL Server ([Más información](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)). | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | Para algunos scripts | Herramienta de línea de comandos para transferir datos con direcciones URL. | [Windows](https://curl.haxx.se/windows/) \| Linux: Instalación de paquete curl |

<sup>1</sup> Debe usar la versión 1.10 o posterior de kubectl. Además, la versión de kubectl debe ser más o menos una versión secundaria del clúster de Kubernetes. Si quiere instalar una versión concreta en el cliente de kubectl, vea [Instalación de kubectl binario mediante curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (en Windows 10, use cmd.exe y no Windows PowerShell para ejecutar curl).

> [!TIP]
> Para usar kubectl con un clúster implementado previamente en Azure Kubernetes Service (AKS), debe establecer el contexto del clúster con el siguiente comando de la CLI de Azure:
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> Debe usar la CLI de Azure versión 2.0.4 o posterior. Ejecute `az --version` para encontrar la versión si fuera necesario.

<sup>3</sup> Si se ejecuta en Windows 10, **curl** ya está en la RUTA DE ACCESO cuando se ejecuta desde un símbolo del sistema cmd. En otras versiones de Windows, descargue **curl** con el vínculo y colóquelo en la RUTA DE ACCESO.

## <a name="which-tools-are-required"></a>Herramientas necesarias

En la tabla anterior se proporcionan todas las herramientas comunes que se usan con clústeres de macrodatos. Las herramientas necesarias dependen del escenario. Pero, en general, las siguientes herramientas son más importantes para administrar, conectarse y consultar el clúster:

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **Extensión SQL Server 2019**

Las herramientas restantes solo son necesarias en determinados escenarios. La **CLI de Azure** se puede usar para administrar servicios de Azure asociados a las implementaciones de AKS. **mssql-cli** es una herramienta opcional, aunque útil, que permite conectarse a la instancia maestra de SQL Server del clúster y ejecutar consultas desde la línea de comandos. Y **sqlcmd** y **curl** son necesarios si piensa instalar datos de ejemplo con el script de GitHub.

### <a id="python"></a> Instalación de Python sin conexión

1. En un equipo con acceso a Internet, descargue uno de los siguientes archivos comprimidos que contienen Python:

   | Sistema operativo | Descargar |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copie el archivo comprimido en el equipo de destino y extráigalo en una carpeta de su elección.

1. Solo para Windows, ejecute `installLocalPythonPackages.bat` desde esa carpeta y pase la ruta de acceso completa a la misma carpeta como un parámetro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc"></a>Descargar e instalar Azure Data Studio versión candidata para lanzamiento de SQL Server 2019 (RC)

Azure Data Studio SQL Server 2019 RC proporciona funciones y características específicas para SQL Server 2019 RC.

En el caso de las versiones de producción normales de Azure Data Studio, siga las instrucciones que aparecen en [descarga e instalación Azure Data Studio](../azure-data-studio/download.md).

|Plataforma|Descargar|Fecha de la versión| Versión |
|:---|:---|:---|:---|
|Windows|[Instalador de usuario (recomendado)](https://go.microsoft.com/fwlink/?linkid=2102435)<br>[Instalador del sistema](https://go.microsoft.com/fwlink/?linkid=2102523)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2102524)|27 de agosto de 2019 |RC 1.11.0: Insiders|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2102436)|27 de agosto de 2019 |RC 1.11.0: Insiders|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2102526)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2102437)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2102525)|27 de agosto de 2019 |RC 1.11.0: Insiders|

Para más información sobre la última versión, consulte las [notas de la versión](../big-data-cluster/release-notes-big-data-cluster.md).

### <a name="get-azure-data-studio-for-windows"></a>Descargar Azure Data Studio para Windows

En esta versión de [!INCLUDE[name-sos](../includes/name-sos-short.md)], se incluye una experiencia de Windows Installer estándar y un archivo .zip.

Le recomendamos que use el *instalador de usuario*, ya que no se necesitan privilegios de administrador, lo que simplifica tanto el proceso de instalación como las actualizaciones. El instalador de usuario no necesita privilegios de administrador porque la ubicación se encuentra en la carpeta AppData local del usuario (LOCALAPPDATA). Además, el instalador de usuario también proporciona una experiencia de actualización en segundo plano más fluida. Para obtener más información, vea [Configuración del usuario para Windows](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows).

**Instalador de usuario** (recomendado)

1. Descargue y ejecute el [instalador de *usuario* de [!INCLUDE[name-sos](../includes/name-sos-short.md)]para Windows](https://go.microsoft.com/fwlink/?linkid=2102435).
2. Inicie la aplicación [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**Instalador del sistema**

1. Descargue y ejecute el [*instalador del sistema* de [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Windows](https://go.microsoft.com/fwlink/?linkid=2102523).
2. Inicie la aplicación [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**archivo zip**

1. Descargue el archivo .zip de [[!INCLUDE[name-sos](../includes/name-sos-short.md)] para Windows](https://go.microsoft.com/fwlink/?linkid=2102524).
2. Busque el archivo descargado y extraiga su contenido.
3. Ejecute `\azuredatastudio-windows\azuredatastudio.exe`:

### <a name="get-azure-data-studio-for-macos"></a>Descargar Azure Data Studio para macOS

1. Descargue [[!INCLUDE[name-sos](../includes/name-sos-short.md)] para macOS](https://go.microsoft.com/fwlink/?linkid=2102436).
2. Para extraer el contenido del archivo zip, haga doble clic en este.
3. Para que [!INCLUDE[name-sos](../includes/name-sos-short.md)] esté disponible en *Launchpad*, arrastre *Azure Data Studio.app* hasta la carpeta *Aplicaciones*.

### <a name="get-azure-data-studio-for-linux"></a>Obtener Azure Data Studio para Linux

1. Descargue [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Linux con uno de los instaladores, o bien descargue el archivo tar.gz:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2102526)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2102437)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2102525)
1. Para extraer el archivo e iniciar [!INCLUDE[name-sos](../includes/name-sos-short.md)], abra una ventana de terminal y escriba los comandos siguientes:

   **Instalación de Debian:**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **Instalación de RPM:**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **Instalación de tar.gz:**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > En Debian, Red Hat y Ubuntu, puede haber dependencias que faltan. Use los siguientes comandos para instalar estas dependencias según la versión de Linux:
   

   **Debian:** 
   ```bash
   sudo apt-get install libunwind8
   ```

   **Redhat:** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```

### <a name="supported-operating-systems"></a>Sistemas operativos admitidos

[!INCLUDE[name-sos](../includes/name-sos-short.md)] se ejecuta en Windows, macOS y Linux, y es compatible con las siguientes plataformas:

#### <a name="windows"></a>Windows

- Windows 10 (64 bits)
- Windows 8.1 (64 bits)
- Windows 8 (64 bits)
- Windows 7 (SP1) 64 bits: se necesita [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

#### <a name="macos"></a>macOS

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Pasos siguientes

Después de configurar las herramientas, implemente un clúster de macrodatos de SQL Server 2019 en Kubernetes en la nube o el entorno local. Para obtener más información, vea los siguientes artículos de implementación:

- [Inicio rápido: Implementación de un clúster de macrodatos de SQL Server en Azure Kubernetes Service (AKS)](quickstart-big-data-cluster-deploy.md)
- [Cómo realizar la [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] implementación en Kubernetes](deployment-guidance.md)

Para obtener más información sobre los clústeres de Big Data, vea [¿Qué son [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
