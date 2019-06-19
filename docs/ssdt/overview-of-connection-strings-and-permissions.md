---
title: Información general acerca de las cadenas de conexión y los permisos | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: ceff114e-a738-46ad-9785-b6647a2247f9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 413d6ad71b70cc4ddca8205589d25e224bbcad76
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65102029"
---
# <a name="overview-of-connection-strings-and-permissions"></a>Información general acerca de las cadenas de conexión y los permisos
Para ejecutar pruebas unitarias de SQL Server, debe conectarse a un servidor de bases de datos mediante una o dos cadenas de conexión específicas. Cada cadena de conexión representa una cuenta que tenga los permisos específicos que necesita para realizar la tarea o el conjunto de tareas en un script determinado como parte de la prueba. Puede especificar estas cadenas en el cuadro de diálogo **Configuración de prueba de SQL Server** o editando manualmente el archivo app.config del proyecto de prueba.  
  
## <a name="connection-strings"></a>Cadenas de conexión  
En el cuadro de diálogo **Configuración de prueba de SQL Server**, puede especificar las cadenas de conexión para cada una de las cuentas siguientes.  
  
> [!NOTE]  
> El contexto de ejecución y el contexto privilegiado solo se diferencian si usa la autenticación de SQL Server. Si usa la autenticación de Windows, se utilizarán las mismas credenciales para ambas cadenas de conexión.  
  
-   Contexto de ejecución (Requerido): Una cuenta de usuario para ejecutar el script de prueba. Esta cadena de conexión debe tener las mismas credenciales que se espera que tengan los usuarios. Esto es importante porque asegura que se hayan aplicado los permisos adecuados a la base de datos. Para más información, vea: [Cómo: Configurar una ejecución de prueba unitaria de SQL Server](../ssdt/how-to-configure-sql-server-unit-test-execution.md).  
  
    En el archivo app.config del proyecto de prueba, es el elemento `ExecutionContext`.  
  
-   Contexto privilegiado (opcional): una cuenta de la misma base de datos con permisos superiores para ejecutar la acción anterior a la prueba, la acción posterior a la prueba, y los scripts TestInitialize y TestCleanup. Estos scripts establecen el estado de la base de datos y, para la acción posterior a la prueba, se pueden usar para validar objetos de la base de datos. Esta cadena de conexión también se usa para implementar los cambios de la base de datos y generar datos.  
  
    En el archivo app.config del proyecto de prueba, es el elemento `PrivilegedContext`. Si las pruebas unitarias de SQL Server ejecutan el script de prueba únicamente, no tiene que especificar un contexto privilegiado.  
  
Las cadenas que especifica en el cuadro de diálogo de configuración del proyecto se almacenan en el archivo app.config del proyecto de prueba. También podría modificar ese archivo directamente y recompilar el proyecto, tras lo cual aparecerán nuevos valores en el cuadro de diálogo.  
  
## <a name="windows-authentication-versus-sql-server-authentication"></a>Autenticación de Windows frente a autenticación de SQL Server  
Al especificar las cadenas de conexión, debe elegir entre el uso de la autenticación de Windows y la autenticación de SQL. Una razón para elegir la autenticación de Windows consiste en que admite mejor que la autenticación de SQL Server el uso de pruebas por parte de un equipo. Si elige la autenticación de SQL Server, las cadenas de conexión se cifran, mediante la API de protección de datos (DPAPI), en función de sus credenciales de usuario. Esto significa que las pruebas de este proyecto de prueba se ejecutarán solo para usted, no para los miembros del equipo que obtienen las pruebas a través del sistema de control de código fuente después de registrarlas. Para ejecutar pruebas en este proyecto de prueba, otros miembros del equipo tendrían que volver a configurar el proyecto de prueba usando sus propias credenciales. Para ello, editarían su copia del archivo app.config o usarían el cuadro de diálogo de configuración del proyecto.  
  
## <a name="permissions"></a>Permisos  
El script de prueba se ejecuta en el nivel de permisos del contexto de ejecución, que es el mismo nivel de permisos que estaría activo para los comandos de usuario que se ejecutan en la base de datos cuando tiene un uso típico. La acción anterior a la prueba, posterior a la prueba y los scripts TestInitialize y TestCleanup se ejecutan en el nivel de permisos del contexto privilegiado.  
  
Debido a la conexión de permiso superior usada para el script de la acción posterior a la prueba, puede realizar la validación en ella. En este script, también puede ejecutar comandos de script que prueban permisos. Para obtener más información acerca de los permisos, vea la sección de pruebas unitarias de SQL Server de [Permisos necesarios para SQL Server Data Tools](../ssdt/required-permissions-for-sql-server-data-tools.md).  
  
## <a name="see-also"></a>Consulte también  
[Crear y definir pruebas unitarias de SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Scripts de pruebas unitarias de SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md)  
[Archivos de prueba unitaria de SQL Server](../ssdt/sql-server-unit-test-files.md)  
  
