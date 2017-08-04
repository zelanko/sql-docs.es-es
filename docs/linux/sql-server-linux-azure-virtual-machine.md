---
title: Aprovisionar un servidor SQL de Linux VM en Azure | Documentos de Microsoft
description: "Este tutorial muestra cómo crear una máquina virtual de Linux de SQL Server 2017 en Azure."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 222e23b2-51e7-429b-b8e5-61e0ebe7df9b
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 0470622b0fe5a8835213617a4fc2e8c74f674873
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-linux-sql-server-2017-virtual-machine-with-the-azure-portal"></a>Crear una máquina virtual de Linux de SQL Server 2017 con el portal de Azure
Azure proporciona imágenes de máquinas virtuales de Linux que tengan instalado SQL Server 2017 RC2. Este tema proporciona un breve tutorial sobre cómo usar el portal de Azure para crear una máquina virtual Linux SQL Server. 

## <a name="create-a-linux-vm-with-sql-server-installed"></a>Crear una VM de Linux con SQL Server instalado

Abra la [portal de Azure](https://portal.azure.com/).

1. Haga clic en **New** a la izquierda.

1. En el **New** hoja, haga clic en **proceso**.

1. Haga clic en **vea todos los** junto a la **aplicaciones destacadas** encabezado.

   ![Vea todas las imágenes de máquina virtual](./media/sql-server-linux-azure-virtual-machine/azure-compute-blade.png)

1. En el cuadro de búsqueda, escriba **SQL Server 2017**y presione **ENTRAR** para iniciar la búsqueda.

    ![Filtro de búsqueda para las imágenes de máquina virtual de SQL Server de 2017](./media/sql-server-linux-azure-virtual-machine/searchfilter.png)

    > [!TIP]
    > Este filtro muestra las imágenes de máquina virtual de Linux disponibles para SQL Server 2017. Con el tiempo, se mostrarán imágenes de SQL Server 2017 para otras distribuciones de Linux compatibles. También puede hacer clic en este [vínculo](https://ms.portal.azure.com/#blade/Microsoft_Azure_Marketplace/GalleryFeaturedMenuItemBlade/selectedMenuItemId/home/searchQuery/sql%20server%202017) para ir directamente a los resultados de búsqueda para SQL Server 2017. 

1. Seleccione una imagen de SQL Server 2017 de los resultados de búsqueda.

1. Haga clic en **Crear**.

1. En el **Fundamentos** hoja, rellene los detalles de la VM de Linux. 

    ![Hoja de conceptos básicos](./media/sql-server-linux-azure-virtual-machine/basics.png)

    > [!Note]
    > Tiene la opción de utilizar una clave pública SSH o una contraseña para la autenticación. SSH es más seguro. Para obtener instrucciones sobre cómo generar una clave SSH, consulte [crear SSH claves en Linux y Mac para máquinas virtuales de Linux en Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-mac-create-ssh-keys). 

1. Haga clic en **Aceptar**.

1. En el **tamaño** hoja, elija un tamaño de la máquina. Para el desarrollo y pruebas funcionales, se recomienda un tamaño de memoria virtual **DS2** o superior. Para las pruebas de rendimiento, use **DS13** o superior.

    ![Elija un tamaño de máquina virtual](./media/sql-server-linux-azure-virtual-machine/vmsizes.png)

    Para ver otros tamaños, seleccione **todas las ver**. Para obtener más información acerca de los tamaños de máquina virtual, consulte [tamaños de VM de Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes).

1. Haga clic en **Seleccionar**.

1. En el **configuración** hoja, puede realizar cambios en la configuración o mantenga la configuración predeterminada.

1. Haga clic en **Aceptar**.

1. En el **resumen** página, haga clic en **Aceptar** para crear la máquina virtual.

> [!NOTE]
> La máquina virtual de Azure previamente configura el firewall para abrir el puerto 1433 de SQL Server para las conexiones remotas. Pero para conectarse de forma remota, también debe agregar una regla de grupo de seguridad de red, como se describe en la sección siguiente.

## <a id="remote"></a>Configurar para las conexiones remotas

Para poder conectarse remotamente a SQL Server en una máquina virtual de Azure, debe configurar una regla de entrada en el grupo de seguridad de red. La regla permite el tráfico en el puerto en el que SQL Server escucha (valor predeterminado de 1433). Los pasos siguientes muestran cómo usar el portal de Azure para este paso. 

1. En el portal, seleccione **máquinas virtuales**y, a continuación, seleccione la VM de SQL Server.

1. En la lista de propiedades, seleccione **interfaces de red**.

1. A continuación, seleccione la interfaz de red para la máquina virtual.

    ![Interfaces de red](./media/sql-server-linux-azure-virtual-machine/networkinterfaces.png)

1. Haga clic en el vínculo de grupo de seguridad de red.

    ![Grupo de seguridad de red](./media/sql-server-linux-azure-virtual-machine/networksecuritygroup.png)

1. En las propiedades del grupo de seguridad de red, seleccione **reglas de seguridad de entrada**.

1. Haga clic en el **+ agregar** botón.

1. Proporcione un nombre de "SQLServerRemoteConnections".

1. En el **servicio** lista, seleccione **MS SQL**.

    ![Regla de grupo de seguridad de MS SQL](./media/sql-server-linux-azure-virtual-machine/sqlnsgrule.png)

1. Haga clic en **Aceptar** para guardar la regla para la máquina virtual.

## <a id="connect"></a>Conéctese a la máquina virtual Linux

Si ya utiliza un shell de BASH, conéctese a la máquina virtual de Azure mediante el **ssh** comando. En el siguiente comando, reemplace el nombre de usuario de la máquina virtual y la dirección IP para conectarse a la VM de Linux.

```bash
ssh -l AzureAdmin 100.55.555.555
```

Puede encontrar la dirección IP de la máquina virtual en el portal de Azure.

![Dirección IP en el portal de Azure](./media/sql-server-linux-azure-virtual-machine/vmproperties.png)

Si se ejecutan en Windows y no tiene un shell de BASH, puede instalar a un cliente de SSH como PuTTY.

1. [Descargue e instale PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. Ejecute PuTTY.

1. En la pantalla de configuración de PuTTY escriba la dirección IP pública de la máquina virtual.

1. Haga clic en Abrir y escriba el nombre de usuario y contraseña en los cuadros.

Para obtener más información sobre cómo conectarse a máquinas virtuales de Linux, consulte [crear una VM de Linux en Azure mediante el Portal de](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-portal#ssh-to-the-vm).

## <a name="configure-sql-server"></a>Configurar SQL Server

1. Después de conectarse a la VM de Linux, abra un nuevo comando terminal.

1. Configurar SQL Server con el siguiente comando.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup 
   ```

   Acepte la licencia y escriba una contraseña para la cuenta de administrador del sistema. Puede iniciar el servidor cuando se le solicite.

1. Si lo desea, [instalar las herramientas de SQL Server](sql-server-linux-setup-tools.md).

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene una máquina virtual de SQL Server 2017 en Azure, puede conectarse localmente con **sqlcmd** para ejecutar consultas Transact-SQL.

Si ha configurado la VM de Azure para las conexiones remotas de SQL Server, también debe ser capaz de conectarse de forma remota. Para obtener un ejemplo de la conexión a SQL Server en Linux desde un equipo remoto de Windows, vea [SSMS de uso en Windows para conectarse a SQL Server en Linux](sql-server-linux-develop-use-ssms.md).

Para obtener más información sobre las máquinas virtuales de Linux en Azure, consulte la [documentación de la máquina Virtual de Linux](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/).

