---
title: MSSQLSERVER_17832 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17828 (Database Engine error)
- maxtokensize
- 17832 (Database Engine error)
- login packet (bad)
ms.assetid: bd56ffe4-0855-4ada-8aca-251fbc6ff2ce
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1280bb44d11ce4f8234d544bf113e796a9c3c85c
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133385"
---
# <a name="mssqlserver17832"></a>MSSQLSERVER_17832
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|17832|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SRV_BAD_LOGIN_PKT|  
|Texto del mensaje|La estructura del paquete de inicio de sesión utilizado para abrir la conexión no es válida; se cerró la conexión. Póngase en contacto con el proveedor de la biblioteca cliente.%.*ls |  
  
## <a name="explanation"></a>Explicación  
 El equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pudo procesar el paquete de inicio de sesión de cliente. Esto puede deberse a que el paquete se creó incorrectamente o a que se dañó durante la transmisión. También puede deberse a la configuración del equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La dirección IP enumerada es la del equipo cliente.  
  
### <a name="more-information"></a>Más información  
 Al utilizar la autenticación de Windows en un entorno de Kerberos, un cliente recibe un vale de Kerberos que contiene un certificado de atributos de privilegios (PAC). El PAC contiene varios tipos de datos de autorización incluidos los grupos de los que el usuario es miembro, los derechos de los que el usuario dispone y qué directivas se le aplican. Cuando el cliente recibe el vale de Kerberos, la información contenida en el PAC se utiliza para generar el token de acceso del usuario. El cliente presenta el token al equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como parte del paquete de inicio de sesión.  
  
 Si el token se creó incorrectamente o se dañó durante la transmisión, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede proporcionar información adicional sobre el problema.  
  
 Cuando el usuario es miembro de muchos grupos o tiene muchas directivas, el token puede crecer más de lo normal como para mostrarlo todo. Si el token aumenta de tamaño por encima del valor de **MaxTokenSize** del equipo servidor, el cliente no puede conectarse, emite un error general de red (GNE) y se puede producir el error 17832. Este problema puede afectar solo a algunos usuarios: los usuarios con muchos grupos o directivas. Cuando el problema es el valor **MaxTokenSize** del equipo servidor, el error 17832 del registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estará acompañado de un error con el estado 9. Para obtener más información sobre Kerberos y **MaxTokenSize**, vea [KB327825](https://support.microsoft.com/kb/327825).  
  
## <a name="user-action"></a>Acción del usuario  
 Para resolver este problema, aumente el valor de **MaxTokenSize** del equipo servidor a un tamaño lo suficientemente grande como para contener el token de mayor tamaño de cualquier usuario de la organización. Para averiguar el tamaño correcto del token para la organización, considere usar la aplicación **Tokensz**.   
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 **Para cambiar el valor de MaxTokenSize en el equipo del servidor**  
  
1.  En el menú **Inicio** , haga clic en **Ejecutar**.  
  
2.  Tipo `regedit`y, a continuación, haga clic en **Aceptar**. (Si aparece el cuadro de diálogo **Control de cuentas de usuario**, haga clic en **Continuar**).  
  
3.  Desplácese a **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa\Kerberos\Parameters**.  
  
4.  Si el parámetro **MaxTokenSize** no está presente, haga clic con el botón derecho en **Parameters**, seleccione **Nuevo** y haga clic en Valor de **DWORD (32 bits)**. Denomine a la entrada del Registro **MaxTokenSize**.  
  
5.  Haga clic con el botón derecho en **MaxTokenSize** y, a continuación, haga clic en **Modificar**.  
  
6.  En el tipo de cuadro **Información del valor**, escriba el valor de **MaxTokenSize** que quiera.  
  
    > [!NOTE]  
    >  El valor ffff hexadecimal (valor decimal 65535) es el tamaño máximo recomendado del token. Si se proporciona este valor, probablemente el problema se resolvería, pero podría tener efectos adversos en todo el equipo con respecto al rendimiento. Recomendamos que establezca el menor valor de **MaxTokenSize** que permita el token de mayor tamaño de cualquier usuario de la organización e introduzca ese valor.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  Cierre el **Editor del Registro**.  
  
9. Reinicie el equipo.  
  
  
