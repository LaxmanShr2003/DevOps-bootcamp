# DevOps Assessment: Package application code into a versioned tarball

Full bash script for packaging the entire application with tar and also including checksum.

#!/bin/bash

set -e  # Exit on error

#############################################

Configuration

#############################################
APP_NAME="TodoBackend"
OUTPUT_DIR="./dist"
REQUIRED_FILES=("package.json" "src")

EXCLUDES=(
"--exclude=node_modules"
"--exclude=.git"
"--exclude=logs"
"--exclude=dist"
"--exclude=env"
"--exclude=.dockerignore"
"--exclude=.prettierrc"
)

#############################################

Validate Require files

#############################################
echo "[*] Validating required files..."

for file in "${REQUIRED_FILES[@]}"; do
if [[ ! -e "$file" ]]; then
echo "[ERROR] Missing required file or directory: $file"
exit 1
fi
done

echo "[OK] All required files exist."

#############################################

Read version from package.json file

#############################################
echo "[*] Reading version from package.json..."

VERSION=$(grep '"version"' package.json | head -1 | awk -F '"' '{print $4}')

if [[ -z "$VERSION" ]]; then
echo "[ERROR] Could not read version from package.json"
exit 1
fi

echo "[OK] Version detected: $VERSION"

TIMESTAMP=$(date +%Y%m%d_%H%M%S)
TARBALL_NAME="${APP_NAME}*${VERSION}*${TIMESTAMP}.tar.gz"

mkdir -p "$OUTPUT_DIR"

#############################################

Build tarball

#############################################
echo "[*] Creating tarball: $TARBALL_NAME"

tar -czf "$OUTPUT_DIR/$TARBALL_NAME" \
"${EXCLUDES[@]}" \
.

echo "[OK] Tarball created."

#############################################

Generate Checksum

#############################################
echo "[*] Generating checksum..."

CHECKSUM_FILE="${TARBALL_NAME}.sha256"
sha256sum "$OUTPUT_DIR/$TARBALL_NAME" > "$OUTPUT_DIR/$CHECKSUM_FILE"

echo "[OK] Checksum generated: $CHECKSUM_FILE"

#############################################

Output

#############################################
echo ""
echo "=========================================="
echo " PACKAGE CREATED SUCCESSFULLY"
echo "=========================================="
echo "Tarball : $OUTPUT_DIR/$TARBALL_NAME"
echo "Checksum: $OUTPUT_DIR/$CHECKSUM_FILE"
echo "=========================================="

## Documentation of code

## **1. Shebang (line 1)**

```bash
#!/bin/bash
```

This tells Linux to run the script using **bash shell**, not sh or zsh.

---

## 🟦 **2. Exit on error**

```bash
set -e
```

Means:

✔ If ANY command fails

✔ The script stops immediately

Prevents creating incomplete/broken packages.

---

## 🟦 **3. Configuration section**

```bash
APP_NAME="TodoBackend"
```

The application name — used in the tarball filename.

Example tarball:

```
TodoBackend_1.0.0_20251127_003401.tar.gz
```

---

```bash
OUTPUT_DIR="./dist"

```

Where the final tar.gz and checksum files will be stored.

---

```bash
REQUIRED_FILES=("package.json" "src")

```

A list of required files/folders your project MUST have.

If any is missing → script stops.

---

```bash
EXCLUDES=(
  "--exclude=node_modules"
  "--exclude=.git"
  "--exclude=logs"
  "--exclude=dist"
  "--exclude=env"
  "--exclude=Dockerfile"
  "--exclude=.dockerignore"
  "--exclude=.prettierrc"
)

```

These tell tar:

❌ Do NOT include these folders/files in the tarball.

Why?

- `node_modules` → very large, should be installed on server
- `.git` → contains repository data, not needed
- `dist` → avoid recursive packaging
- `Dockerfile`, `.prettierrc` → not needed for runtime

---

# 🟦 **4. Validating required files**

```bash
echo "[*] Validating required files..."

```

Just prints a message.

---

```bash
for file in "${REQUIRED_FILES[@]}"; do
  if [[ ! -e "$file" ]]; then
    echo "[ERROR] Missing required file or directory: $file"
    exit 1
  fi
done

```

Loop through each item in REQUIRED_FILES:

- If the file does NOT exist → show error → exit script.

Purpose:

To ensure your project is valid before packaging.

---

```bash
echo "[OK] All required files exist."

```

Confirmation.

---

# 🟦 **5. Reading version from package.json**

```bash
echo "[*] Reading version from package.json..."

```

Informational.

---

```bash
VERSION=$(grep '"version"' package.json | head -1 | awk -F '"' '{print $4}')

```

This extracts version number from package.json.

Example package.json:

```json
"version": "1.0.0"

```

So VERSION becomes:

```
1.0.0
```

Breakdown:

- `grep "version"` → find the line
- `head -1` → first occurrence
- `awk -F '"' '{print $4}'` → split by `"`, take 4th element (the actual number)

---

```bash
if [[ -z "$VERSION" ]]; then
  echo "[ERROR] Could not read version from package.json"
  exit 1
fi

```

If version not found → error → stop.

---

```bash
echo "[OK] Version detected: $VERSION"
```

Confirmation.

---

```bash
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
```

Generates timestamp like:

```
20251127_003401

```

Used to ensure each tarball has a unique name.

---

```bash
TARBALL_NAME="${APP_NAME}_${VERSION}_${TIMESTAMP}.tar.gz"

```

Final tarball name example:

```
TodoBackend_1.0.0_20251127_003401.tar.gz

```

---

```bash
mkdir -p "$OUTPUT_DIR"

```

Creates the `dist` directory if it doesn't exist.

---

# 🟦 **6. Creating the tarball**

```bash
echo "[*] Creating tarball: $TARBALL_NAME"

```

---

```bash
tar -czf "$OUTPUT_DIR/$TARBALL_NAME" \
  "${EXCLUDES[@]}" \
  .

```

This is the main packaging command.

Breakdown:

- `tar` → archive tool
- `c` → create new archive
- `z` → compress using gzip
- `f` → output filename

`.` means "take everything from current directory".

`"${EXCLUDES[@]}"` adds all exclude rules.

---

```bash
echo "[OK] Tarball created."

```

---

# 🟦 **7. Generate checksum**

```bash
echo "[*] Generating checksum..."

```

---

```bash
CHECKSUM_FILE="${TARBALL_NAME}.sha256"
```

Example:

```
TodoBackend_1.0.0_20251127_003401.tar.gz.sha256
```

---

```bash
sha256sum "$OUTPUT_DIR/$TARBALL_NAME" > "$OUTPUT_DIR/$CHECKSUM_FILE"
```

Computes SHA-256 hash for verification.

Useful when sending the package to server.

---

```bash
echo "[OK] Checksum generated: $CHECKSUM_FILE"
```

---

# 🟦 **8. Final output**

```bash
echo ""
echo "=========================================="
echo " PACKAGE CREATED SUCCESSFULLY"
echo "=========================================="
echo "Tarball : $OUTPUT_DIR/$TARBALL_NAME"
echo "Checksum: $OUTPUT_DIR/$CHECKSUM_FILE"
echo "=========================================="
```

Nice clean output for the user.

---

# ✅ Summary

script:

1. Checks required files
2. Reads version from package.json
3. Builds name using version + timestamp
4. Packages the code
5. Excludes not required directories
6. Generates checksum
7. Prints final paths