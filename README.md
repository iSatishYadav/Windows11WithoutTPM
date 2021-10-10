# How to Install Windows 11 on unsupported Devices - Officially - No Crack - No 3rd Party Tool
So you wanted the new Windows 11 everyone's talking about, but got a dreadful message liked that:

> This PC doesn't currently meet Windows 11 system requirements:

Unfortunately, you're not one of the lucky ones. Don't worry, we'll figure out a way together.

> Check the [Microsof's Official System Requirements for Windows 11](https://www.microsoft.com/en-in/windows/windows-11-specifications).

Now let's see how can you still install Windows 11. The answer is, of course - it depends. On what you don't have.

I've categorized into 3 reason:

1. You don't have `TPM` 2.0 (but do have 1.2 or other).
2. You don't have any `TPM`. But do have `Secure Boot`. 
3. You don't even have `Secure Boot`.

> What is `TPM (Trusted Platform Module)`

How to find out which one do you have? Here's how, type following command on your `Command Prompt` or `Run`

````shell
tpm.msc
````
If you don't have any `TPM`, following screen should pop up.

![image](https://user-images.githubusercontent.com/4049421/136685013-61d97061-b607-405d-add5-1db05f01370e.png)

Otherwise, details of your `TPM` would show up.

Now, back to our solutions.

## Solutions based on what you're missing

### 1. You don't have `TPM` 2.0 (but do have `TPM` 1.2 or other)
Things are easier when you have some sort of `TPM` e.g. 1.2 (but not 2.0). You just need to tell Windows - not to check for TPM 2.0. Wait, what? Yes!

The usual disclaimer from Microsoft:
> Serious problems might occur if you modify the registry incorrectly by using Registry Editor or by using another method. These problems might require that you reinstall the operating system. Microsoft cannot guarantee that these problems can be solved. Modify the registry at your own risk.

1. 1. Add the following registry setting in your existing Windows 10 Registry Editor:

````shell
Registry Key: HKEY_LOCAL_MACHINE\SYSTEM\Setup\MoSetup

Name: AllowUpgradesWithUnsupportedTPMOrCPU

Type: REG_DWORD

Value: 1
````

Should look like this:

![image](https://user-images.githubusercontent.com/4049421/136685620-41497072-ba44-4bd5-a9de-53d4936e2b25.png)

1.2. Go to Windows 11 [Create Windows 11 installation media](https://www.microsoft.com/en-us/software-download/windows11) page and follow the Official Instructions to create Bootable Media.
1.3. Boot from this new media and you're good to go.

### 2. If you don't have a any `TPM`
Follow the step #1.1 and step #1.2. But before booting from the new media, make note of follwing.

> You need to change one more registry setting, not on your current Windows Installation, but after you boot from your new media. I'd recommend to open this blog post in another device for reference, or note it down.

Since you don't have any sort of `TPM`, add follwoing registry after booting from new media and BEFORE proceeding to "Install Now".

2.1. Press Shift+F10 to open a `Command Prompt`. Open registry editor by typing `regedit`.
2.2. Add new registry key named `LabConfig`.

![image](https://user-images.githubusercontent.com/4049421/136686065-86d63f79-860a-4698-b2b0-092b04599dc9.png)

2.3 Add new `DWORD` named `BypassTMPCheck` and change the value to `1`.

![image](https://user-images.githubusercontent.com/4049421/136686133-adac3bcf-bfa6-4adf-94bb-6d1182e0f29c.png)

2.4 Continue with the setup.

### 3. If you don't have Secure Boot
3.1. Follow till step# 2.3 and add a `DWORD` named `BypassSecureBootCheck` and change the value to `1`.

![image](https://user-images.githubusercontent.com/4049421/136686188-1b852754-6acc-4194-8d48-26a5e74c2a7c.png)

3.2. Continue with the setup.

And that's it! That wasn't so bad, right?

## Disclaimer
Even though I've personally tested the instruction on my personal Windows 10 machine (without any TPM, but with Secure Boot). I am by no means responsible for any damage resulted by following instructions.

Originally posted at https://blog.satishyadav.com.
