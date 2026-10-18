import os, zipfile

base = "/mnt/data/BalkanEmpire_Purple_End"
os.makedirs(base + "/data/balkanempire/function", exist_ok=True)
os.makedirs(base + "/data/minecraft/tags/function", exist_ok=True)

cmds = [
    "gamerule commandBlockOutput false",
    "gamerule doDaylightCycle false",
    "time set midnight",
    "weather clear",
]
# Layered 500x500 floating platform in 25-block strips
for x in range(-250, 250, 25):
    x2 = x + 24
    cmds += [
        f"fill {x} 60 -250 {x2} 60 249 crying_obsidian replace air",
        f"fill {x} 61 -250 {x2} 61 249 purpur_block replace air",
        f"fill {x} 62 -250 {x2} 62 249 end_stone_bricks replace air",
    ]
cmds += [
    "fill -250 63 -250 249 66 -246 crying_obsidian",
    "fill -250 63 246 249 66 250 crying_obsidian",
    "fill -250 63 -245 -246 66 245 crying_obsidian",
    "fill 246 63 -245 250 66 245 crying_obsidian",
    "fill -249 67 -249 248 67 -248 sea_lantern",
    "fill -249 67 248 248 67 249 sea_lantern",
    "fill -249 67 -247 -248 67 247 amethyst_block",
    "fill 248 67 -247 249 67 247 amethyst_block",
]
for y, block, r in [
    (63, "polished_blackstone_bricks", 45),
    (64, "crying_obsidian", 40),
    (65, "purpur_block", 35),
    (66, "end_stone_bricks", 30),
]:
    cmds.append(f"fill {-r} {y} {-r} {r} {y} {r} {block}")
cmds += [
    "fill -3 67 -34 3 67 34 purple_concrete",
    "fill -34 67 -3 34 67 3 purple_concrete",
    "fill -2 68 -2 2 68 2 sea_lantern",
]
for x, z, h in [
    (-120, -120, 24), (120, -120, 30), (-120, 120, 28), (120, 120, 22),
    (-170, 0, 18), (170, 0, 26), (0, -170, 25), (0, 170, 20)
]:
    cmds += [
        f"fill {x-5} 63 {z-5} {x+5} 64 {z+5} obsidian",
        f"fill {x-3} 65 {z-3} {x+3} {65+h//2} {z+3} crying_obsidian",
        f"fill {x-2} {66+h//2} {z-2} {x+2} {66+h//2+3} {z+2} amethyst_block",
        f"fill {x} {66+h//2+4} {z} {x} {65+h} {z} purple_stained_glass",
        f"setblock {x} {66+h} {z} end_rod",
    ]
cmds += [
    "fill -12 63 -12 12 63 12 polished_blackstone_bricks",
    "fill -9 64 -9 9 64 9 purpur_block",
    "fill -6 65 -6 6 65 6 amethyst_block",
    "setblock 0 66 0 beacon",
    "setblock 0 67 0 end_rod",
    "setblock 0 64 10 respawn_anchor",
    "setblock 0 64 -10 respawn_anchor",
    "setblock 10 64 0 respawn_anchor",
    "setblock -10 64 0 respawn_anchor",
    "setworldspawn 0 68 0",
]
for x, z in [(-55, 0), (55, 0), (0, -55), (0, 55)]:
    cmds += [
        f"fill {x-4} 64 {z-4} {x+4} 64 {z+4} crying_obsidian",
        f"fill {x-3} 65 {z-3} {x+3} 70 {z+3} air",
        f"fill {x-3} 65 {z-3} {x-2} 72 {z+3} amethyst_block",
        f"fill {x+2} 65 {z-3} {x+3} 72 {z+3} amethyst_block",
        f"fill {x-1} 71 {z-3} {x+1} 72 {z-3} purple_stained_glass",
    ]

with open(base + "/data/balkanempire/function/build.mcfunction", "w", encoding="utf-8") as f:
    f.write("\n".join(cmds) + "\n")
with open(base + "/pack.mcmeta", "w", encoding="utf-8") as f:
    f.write('{"pack":{"pack_format":94,"description":"BalkanEmpire Purple End PvP Arena"}}\n')
with open(base + "/data/minecraft/tags/function/load.json", "w", encoding="utf-8") as f:
    f.write('{"values":[]}\n')
with open(base + "/README.txt", "w", encoding="utf-8") as f:
    f.write("""BALKANEMPIRE PURPLE END — Aternos setup
Minecraft Java 1.21.11

This ZIP is a datapack builder, not a pre-generated world save. It builds the
500x500 Purple End arena in the End dimension when you run its function.

1. Make a backup of your world first.
2. Upload this ZIP as a datapack into world/datapacks/ (the ZIP root must contain
   pack.mcmeta and data/). If Aternos's file manager does not support this, upload
   through the world's Files page if available, or download the world and add it
   locally before uploading it again.
3. Restart the server.
4. In the End dimension, run as OP: /function balkanempire:build
5. Teleport to the center: /execute in minecraft:the_end run tp @s 0 75 0

Run the function only once. It creates a floating purple End platform, central
PvP arena, crystal towers, glowing perimeter and spawn hub.
""")

zip_path = "/mnt/data/BalkanEmpire_Purple_End_Aternos.zip"
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as z:
    for root, dirs, files in os.walk(base):
        for name in files:
            p = os.path.join(root, name)
            z.write(os.path.join(root, name), os.path.relpath(os.path.join(root, name), base))
print("Created:", zip_path, "size:", os.path.getsize(zip_path), "commands:", len(cmds))
