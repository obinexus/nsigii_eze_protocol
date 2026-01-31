# NSIGII RIFT V1 Architecture
## OBINexus Operation Service Framework

### Schema: `obinexus.[operation].[service]`

---

## Core Philosophy

**All squares are rectangles, not all rectangles are squares.**  
**All drivers are binders, not all drivers execute logic.**  
**Implicit RIFT means explicit RIFT policies.**

---

## System Architecture

### 1. Color Verification Layers

**Primary Colors:**
- **RED**: Incoming data stream
- **GREEN**: Verification layer
- **BLUE**: Outgoing/moving data

**Secondary Colors:**
- **CYAN** (RED + GREEN): 1/2 shared verification (1/4 + 1/4)
- **YELLOW**: Warning/transition state
- **MAGENTA**: Critical boundary
- **BLACK**: Null/terminated state
- **CONTRAST_INVERSE**: Polarity inversion for dual-path verification

### 2. AUX Instruction Sequence

```
AUX_NOSIGNAL → Half-start sequence
AUX_SIGNAL   → Dual-start sequence
AUX_START    → Full initialization
AUX_STOP     → Termination with context preservation
```

**Noise Management:**
- `NOISE_AUX_START`: High-entropy initialization
- `NONOISE_AUX_START`: Low-entropy/deterministic start

**Principle:** AUX instructions represent half of the full instruction in sequence series for signal processing of imagery bytes.

---

## RIFT Stage Architecture

### Stage 000-111: Lexer (Memory Encoding)
**File Types:** `.mrf` (meta rift), `.rf` (rift)

**Token Triplet Structure:**
```c
typedef struct {
    TokenType type;      // Relation: What it is
    uint32_t memory;     // Memory pointer: Where it lives
    uint32_t value;      // Value/length: What it contains
} TokenTriplet;
```

**Memory Tree:** Binary tree with right-child encoding (0 or 1 via memory_code)

### Stage 222: Parser (Canonical Tomography)
**File Type:** `.mrf` (metarift files for all canonical tomography)

**Tomographic Indexing:**
- Six permutations: `ijk, jik, ikj, jki, kij, kji`
- Row-column coherence verification
- Polarity-aligned matrix scanning

### Stage 333: Semantic Analysis (Shared AST)
**Target:** Protocol-agnostic Abstract Syntax Tree

**Objective:**
- Create unified AST for Python, Go, Lua, C, C++, C#
- Object-based role action verification
- Type-memory-value coherence checking

---

## CISCO Protocol (Real-Time Balance Verification)

**CISCO = Eulerian Bottom-up Self-Balancing Tree Augmented Trie Node Chain**

**Properties:**
- Platform-independent instruction aux start/stop
- Real-time RED-GREEN-BLUE verification
- Self-balancing during token insertion
- Eulerian path for optimal traversal

**Verification Cycle:**
```
RED input → GREEN verify → BLUE output
         ↓
      CYAN (1/2 shared consensus)
```

---

## File Structure

```
NSIGII_RIFT_V1JAN2026/
├── c/
│   ├── src/
│   │   ├── tokenizer.c
│   │   ├── parser.c
│   │   ├── nsigii_core.c
│   │   ├── phantom_encoder.c
│   │   └── cisco_balance.c
│   └── include/
│       └── service/
│           ├── nsigii.h
│           ├── rift_stages.h
│           └── color_verify.h
├── cpp/
│   └── src/ (same structure)
├── csharp/
│   └── src/ (same structure)
├── python/
│   ├── setup.toml
│   └── nsigii/
│       ├── __init__.py
│       ├── rift_binding.py
│       └── phantom_id.py
├── go/
│   ├── go.mod
│   └── nsigii/
│       └── rift.go
├── lua/
│   ├── nsigii-1.0-1.rockspec
│   └── nsigii.lua
└── riftfiles/
    ├── *.mrf (metacanonical files)
    └── *.rf (physical rift stage files)
```

---

## Zero Trust Phantom Decoder Integration

**Phantom ID Properties:**
- Salt-based cryptographic identity
- Derived IDs for purpose separation
- Zero-knowledge verification
- No storage of raw identity data

**RIFT Integration:**
```c
phantom_id_t generate_token_identity(TokenTriplet* token);
bool verify_token_phantom(phantom_id_t id, verification_key_t key);
```

---

## Service Definition Schema

```
obinexus.tokenize.lexer      // Stage 000-111
obinexus.parse.syntax         // Stage 222
obinexus.analyze.semantic     // Stage 333
obinexus.verify.color         // RGB verification
obinexus.balance.cisco        // Tree balancing
obinexus.encode.phantom       // Identity management
```

---

## Build Targets

**Required Outputs:**
1. **C Library**: `libnsigii_rift.a` / `libnsigii_rift.so`
2. **C++ Library**: `libnsigii_rift.so` (with C++ bindings)
3. **C# Assembly**: `NSigii.Rift.dll`
4. **Python Package**: `nsigii-rift` (via PyTOML)
5. **Go Module**: `github.com/obinexus/nsigii-rift`
6. **Lua Rock**: `nsigii-rift-1.0-1.lua`

**Binding Strategy:**
- FFI (Foreign Function Interface) for dynamic languages
- Direct compilation for C/C++/C#
- SWIG wrappers where necessary

---

## Parser Unification

**Goal:** Single parser for C, C++, C#

**Strategy:**
- Common `.mrf` metacanonical representation
- Language-specific emission in Stage 333
- Shared semantic validation core

**Canonical Matching:**
```
C:      int x = 5;
C++:    int x = 5;
C#:     int x = 5;
MRF:    <decl type="int" id="x" value="5"/>
```
