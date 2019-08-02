---
title: Instalación de las características de lenguaje R y Python en una máquina virtual de Azure
description: Ejecute soluciones de ciencia de datos y aprendizaje automático de R y Python en una máquina virtual de SQL Server en la nube de Azure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b7aa37c3ec72390d76ecf9e939916f9641187956
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715883"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>Instalación de Machine Learning Services de SQL Server con R y Python en una máquina virtual de Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Puede instalar la integración de R y Python con Machine Learning Services en una máquina virtual SQL Server en Azure, lo que elimina las tareas de instalación y configuración. Una vez implementada la máquina virtual, las características están listas para su uso.
 
Para obtener instrucciones paso a paso, vea [Cómo aprovisionar una máquina virtual de Windows SQL Server en el Azure portal](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision).

El paso [configurar las opciones de SQL Server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings) es donde se agrega el aprendizaje automático a la instancia.

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>Desbloqueo del firewall

De forma predeterminada, el Firewall de la máquina virtual de Azure incluye una regla que bloquea el acceso a la red para las cuentas de usuario locales.

Debe deshabilitar esta regla para asegurarse de que puede tener acceso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la instancia desde un cliente de ciencia de datos remoto.  De lo contrario, el código de machine learning no se puede ejecutar en contextos de proceso que usan el área de trabajo de la máquina virtual.

Para habilitar el acceso desde clientes de ciencia de datos remotos:

1. En la máquina virtual, abra Firewall de Windows con seguridad avanzada.
2. Seleccione **Reglas de salida**.
3. Deshabilite la siguiente regla:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>Habilitar devoluciones de llamada ODBC para clientes remotos

Si espera que los clientes que llaman al servidor necesiten emitir consultas ODBC como parte de sus soluciones de aprendizaje automático, debe asegurarse de que Launchpad pueda realizar llamadas ODBC en nombre del cliente remoto. 

Para ello, debe permitir que las cuentas de trabajo SQL que usan Launchpad puedan iniciar sesión en la instancia. Para obtener más información, vea [Agregar SQLRUserGroup como un usuario de base de datos](../security/create-a-login-for-sqlrusergroup.md).

<a name="network"></a>

## <a name="add-network-protocols"></a>Agregar protocolos de red

+ Habilitar las canalizaciones con nombre
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa el protocolo Canalizaciones con nombre en las conexiones entre los equipos cliente y servidor, así como en algunas conexiones de naturaleza interna. Si Canalizaciones con nombre no está habilitado, debe instalarlo y habilitarlo tanto en la máquina virtual de Azure como en cualquier cliente de ciencia de datos que se conecte al servidor.
  
+ Habilitar TCP/IP

  TCP/IP es necesario para las conexiones de bucle invertido. Si obtiene el error "DBNETLIB; SQL Server no existe o se ha denegado el acceso ", habilite TCP/IP en la máquina virtual que admite la instancia.