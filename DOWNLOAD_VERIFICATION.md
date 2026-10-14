# Verifying your GridSight download

GridSight is free and closed-source, and the EXE is **not code-signed**. That means Windows cannot tell you who made the
file. These steps let you check that the file you have is exactly the one the author published.

## 1. Download from the official place only

Only from **https://github.com/evelens-app/evelens/releases**. Do not run copies from Discord, forums, file-sharing sites or
friends — even if the name is the same.

## 2. Check the SHA-256 before the first run

1. Open the folder with `GridSight.exe`.
2. Right-click an empty area → **Open in Terminal** (or open PowerShell and `cd` to the folder).
3. Run:
   ```powershell
   Get-FileHash .\GridSight.exe -Algorithm SHA256
   ```
4. Compare the result with the SHA-256 in the release notes of the version you downloaded. **Every character must match**
   (upper/lower case does not matter).

If it does not match: delete the file and download again from GitHub Releases. If it still does not match, do not run it —
please report it privately (see SECURITY.md).

Optional extra checks:
- File → Properties → **Details** → *Product version* must show the version of the release you downloaded (and the build
  commit, if the release notes list one).
- If the author also posts the hash outside GitHub (for example in a forum thread), compare it there too — a second
  place makes a swapped file harder to hide.

## 3. "Windows protected your PC" (SmartScreen)

Windows shows this for **new files without a digital signature or download history**. It does not mean malware was found;
it means Windows does not know the file yet. Publisher will show as *Unknown publisher*.

If the hash matched and you decide to run it: click **More info → Run anyway**.

If your PC is managed by an organization, or Windows/your antivirus **blocks** the file with no "Run anyway" option, that is
a policy decision on your PC — **do not try to bypass it**, and do not disable protection. Ask your administrator or don't
use GridSight on that PC.

## 4. Antivirus warnings

Some antivirus programs are suspicious of new unsigned files and of features GridSight really uses (a single-file EXE that
unpacks its runtime to `%TEMP%`, optional autostart, Windows performance tracing for FPS, global hotkeys). What GridSight
does with your system is listed in [SECURITY.md](SECURITY.md) and [PRIVACY.md](PRIVACY.md).

If your antivirus flags GridSight:
- Check the hash first (step 2). A mismatched file is a real problem.
- With a matching hash, you can submit the file to your antivirus vendor as a possible false positive using the vendor's
  official form, and let us know (Issues — no need to keep this private).
- Never disable your antivirus to run GridSight.

## 5. What a matching hash does and does not prove

- ✔ The file is byte-for-byte the one published in the release.
- ✘ It does not prove the file is safe or that the source code does what the documentation says. Read SECURITY.md (limits)
  and decide for yourself. A VirusTotal result, if one is linked, is only a signature check by antivirus engines.
