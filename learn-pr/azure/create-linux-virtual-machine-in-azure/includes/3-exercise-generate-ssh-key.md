Before we can create a Linux virtual machine in Azure, we'll need to think about remote access. We want to be able to sign in to our Linux web server to configure the software and perform maintenance. The default approach to administering Linux VMs hosted in Azure is SSH.

## What is SSH?

Secure Shell (SSH) is an encrypted connection protocol that allows secure sign-ins over unsecured connections. SSH allows you to connect to a terminal shell from a remote location using a network connection.

There are two approaches we can use to authenticate an SSH connection: **username and password**, or an **SSH key pair**.

Although SSH provides an encrypted connection, using passwords with SSH connections leaves the VM vulnerable to brute-force attacks of passwords. A more secure and preferred method of connecting to a Linux VM with SSH is a public-private key pair, also known as SSH keys.

With an SSH key pair, you can sign in to Linux-based Azure virtual machines without a password. This is a more secure approach if you only plan to sign in to the VM from a few computers. If you need to be able to access the Linux VM from a variety of locations, a username and password combination might be a better approach. There are two parts to an SSH key pair: a public key and a private key.

* The public key is placed on your Linux VM or any other service that you wish to use with public-key cryptography. This can be shared with anyone.

* The **private key** is what you present to verify your identity to your Linux VM when you make an SSH connection. Consider this confidential information and protect it like you would a password or any other private data.

You can use the same single public-private key pair to access multiple Azure VMs and services.

## Create the SSH key pair

On Windows 10, Windows 11, Linux, and macOS, you can use the built-in `ssh-keygen` command to generate the SSH public and private key files.

Windows 10 includes an SSH client with the **Fall Creators Update**. Windows 11 includes an SSH client by default. Earlier versions of Windows require additional software to use SSH; [check the documentation for full details](/azure/virtual-machines/linux/ssh-from-windows). Alternatively, you can install the Linux subsystem for Windows and get the same functionality.

We'll use Azure Cloud Shell, which stores the generated keys in Azure in your private storage account. You can also type these commands directly into your local shell if you prefer. You'll need to adjust the instructions throughout this module to reflect a local session if you take this approach.

Here's the minimum command necessary to generate the key pair for an Azure VM. This creates an SSH protocol 2 (SSH-2) RSA public-private key pair. The minimum length is 2048, but for the sake of this learning module, we'll use 4096.

1. Run the following command in Cloud Shell.

   ```bash
   ssh-keygen -m PEM -t rsa -b 4096
   ```

2. Press <kbd>Enter</kbd> to accept the default location. The command creates two files: `id_rsa` and `id_rsa.pub` in the `~/.ssh` directory. The files are overwritten if they exist.

3. Enter a passphrase that you'll remember. You'll need this passphrase when you use the SSH key to access the VM.

There are various options you can use to provide the file name or a passphrase to avoid the prompts.

### Private key passphrase

You can provide a passphrase while generating your private key. This is a password you must enter when you use the key. This passphrase is used to access the private SSH key file and isn't the user account password.

When you add a passphrase to your SSH key, it encrypts the private key using 128-bit AES so that the private key is useless without the passphrase to decrypt it.

We strongly recommended that you add a passphrase. If an attacker stole your private key and that key didn't have a passphrase, they would be able to use that private key to log in to any servers that have the corresponding public key. If a passphrase protects a private key, that attacker can't use it. This provides an additional layer of security for your infrastructure on Azure.

## Use the SSH key pair with an Azure Linux VM

After you have the key pair generated, you can use it with a Linux VM in Azure. You can supply the public key during the VM creation, or add it after the VM has been created.

You can view the contents of the file in Cloud Shell by running the following command.

```bash
cat ~/.ssh/id_rsa.pub
```

It will look something like the following output:

```output
ssh-rsa XXXXXXXXXXc2EAAAADAXABAAABAXC5Am7+fGZ+5zXBGgXS6GUvmsXCLGc7tX7/rViXk3+eShZzaXnt75gUmT1I2f75zFn2hlAIDGKWf4g12KWcZxy81TniUOTjUsVlwPymXUXxESL/UfJKfbdstBhTOdy5EG9rYWA0K43SJmwPhH28BpoLfXXXXXGX/ilsXXXXXKgRLiJ2W19MzXHp8z3Lxw7r9wx3HaVlP4XiFv9U4hGcp8RMI1MP1nNesFlOBpG4pV2bJRBTXNXeY4l6F8WZ3C4kuf8XxOo08mXaTpvZ3T1841altmNTZCcPkXuMrBjYSJbA8npoXAXNwiivyoe3X2KMXXXXXdXXXXXXXXXXCXXXXX/ azureuser@myserver
```

Copy this value so you can use it in the next exercise.

### Use the SSH key when creating a Linux VM

To apply the SSH key while creating a new Linux VM, copy the contents of the public key and supply it to the Azure portal, _or_ supply the public key file to the Azure CLI or Azure PowerShell command. We'll use this approach when we create our Linux VM.

### Add the SSH key to an existing Linux VM

If you've already created a VM, you can install the public key onto your Linux VM with the `ssh-copy-id` command. After the key has been authorized for SSH, it grants access to the server without a password, though you'll still be prompted for the passphrase on the key if you set one.

For example, if we had a Linux VM named *myserver* with a user *azureuser*, we could run the following command to install the public key file, and authorize the user with the key.

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub azureuser@myserver
```

Now that we have our public key, let's switch to the Azure portal and create a Linux VM.