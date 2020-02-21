---
title: Ejemplo que muestra el uso del proveedor de Azure Key Vault con Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: fca498fbc7f79dcfc8852799ade6e230952ea082
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75250953"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted"></a>Ejemplo que muestra el uso del proveedor de Azure Key Vault con Always Encrypted

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-xxxx-md.md)]

En este ejemplo se muestra el uso del proveedor de Azure Key Vault proveedor al obtener acceso a las columnas cifradas.

[!code-csharp [AKVProvider Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderExample.cs#1)]

## <a name="see-also"></a>Consulte también

- [Ejemplo que muestra el uso del proveedor de Azure Key Vault con Always Encrypted habilitado con enclaves seguros](azure-key-vault-enclave-example.md)
- [Tutorial: Desarrollo de una aplicación de .NET mediante Always Encrypted con enclaves seguros](tutorial-always-encrypted-enclaves-develop-net-apps.md)
- [Uso de Always Encrypted con el proveedor de datos Microsoft .NET para SQL Server](sqlclient-support-always-encrypted.md)
