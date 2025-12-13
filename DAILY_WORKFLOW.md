# 📅 Daily Workflow Guide

## Adding New Day's Data

When you run a new simulation each day, follow these simple steps:

### Step 1: Create the New Data File
```bash
# Create a new file for today's data (example for day 2)
nano data_day_2.jsonl

# Or if you prefer copying the structure:
touch data_day_2.jsonl
```

### Step 2: Copy/Paste Your Simulation Data
- Run your simulation
- Copy all the JSONL output
- Paste it into your new `data_day_X.jsonl` file
- Save and close

### Step 3: Update main.rs
Open `src/main.rs` and find the data_files section (around line 15). 

**Uncomment the line for your new day:**

```rust
let data_files = vec![
    "research_data.jsonl",      // Original data
    "src/data_day_1.jsonl",     // Day 1
    "data_day_2.jsonl",         // Day 2 - UNCOMMENT THIS!
    // "data_day_3.jsonl",       // Day 3 - uncomment when ready
];
```

### Step 4: Run ChronoDB
```bash
cargo run
```

That's it! Your new data is now loaded and analyzed. 🎉

---

## 📊 File Naming Convention

**Recommended naming:**
```
research_data.jsonl      ← Original/test data
data_day_1.jsonl         ← Day 1 (or keep in src/data_day_1.jsonl)
data_day_2.jsonl         ← Day 2
data_day_3.jsonl         ← Day 3
...and so on
```

**Or organized by date:**
```
data_2025_12_06.jsonl    ← December 6, 2025
data_2025_12_07.jsonl    ← December 7, 2025
data_2025_12_08.jsonl    ← December 8, 2025
```

---

## 🔍 Quick Check Commands

### See what files you have:
```bash
ls -lh data_day_*.jsonl
```

### Count entries in a file:
```bash
wc -l data_day_2.jsonl
```

### Preview first 5 entries:
```bash
head -5 data_day_2.jsonl
```

---

## ⚡ Pro Tips

### 1. **Backup Strategy**
Keep your data files safe:
```bash
# Create a backup folder
mkdir -p backups

# Copy today's data
cp data_day_2.jsonl backups/data_day_2_backup.jsonl
```

### 2. **Quick Load Test**
Test a new file before adding to main.rs:
```bash
# Just check if it's valid JSON
jq empty < data_day_2.jsonl 2>&1 | head -10
```

### 3. **Load Only Recent Days**
If your database gets huge, you can comment out older days:
```rust
let data_files = vec![
    // "research_data.jsonl",   // Archived
    // "data_day_1.jsonl",      // Archived
    "data_day_2.jsonl",         // Keep recent
    "data_day_3.jsonl",         // Keep recent
];
```

---

## 🛠️ Troubleshooting

### Problem: "File not found" error
**Solution:** Check your file path. Files should be in `/home/labrat/rusted_out/` directory.

```bash
# Check where you are
pwd

# Should show: /home/labrat/rusted_out
# If not, navigate there:
cd /home/labrat/rusted_out
```

### Problem: Some entries skip/fail to load
**Solution:** This is normal! ChronoDB automatically skips malformed entries and reports them. Check the output to see which lines had issues.

### Problem: Database is slow with many days
**Solution:** 
1. Consider archiving old days (comment them out in main.rs)
2. Or implement the binary persistence feature (see ARCHITECTURE.md)

---

## 📈 Example Timeline

**Week 1:**
```
Day 1: data_day_1.jsonl (1,057 entries)
Day 2: data_day_2.jsonl (1,100 entries)
Day 3: data_day_3.jsonl (1,089 entries)
...
Total: ~3,246 entries
```

**Month 1:**
```
30 days × ~1,100 entries = ~33,000 entries
Still very fast in memory! ⚡
```

---

## 🎯 Quick Reference

| Task | Command |
|------|---------|
| Create new day file | `nano data_day_X.jsonl` |
| Edit main.rs | `nano src/main.rs` |
| Run ChronoDB | `cargo run` |
| List all data files | `ls -lh data_day_*.jsonl` |
| Count entries | `wc -l data_day_X.jsonl` |

---

## 🚀 Next Steps

After you've loaded a few days:
1. Try comparing agent activity across days
2. Look for trends in research depth
3. Track how task focus changes over time
4. Search for specific topics across all days

Check out `QUICKSTART.md` for query examples!
