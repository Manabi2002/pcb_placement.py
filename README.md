import matplotlib.pyplot as plt
import matplotlib.patches as patches
import math

BOARD_SIZE = 50
)
COMPONENTS = {
    "USB": (5, 5),
    "MICROCONTROLLER": (5, 5),
    "CRYSTAL": (5, 5),
    "MIKROBUS1": (5, 15),
    "MIKROBUS2": (5, 15),
}

def draw_component(ax, name, x, y, w, h, color):
    rect = patches.Rectangle((x, y), w, h, linewidth=2,
                             edgecolor="black", facecolor=color, alpha=0.8)
    ax.add_patch(rect)
    ax.text(x + w/2, y + h/2, name, ha="center", va="center", fontsize=8, color="white")

def distance(p1, p2):
    return math.sqrt((p1[0]-p2[0])**2 + (p1[1]-p2[1])**2)

def main():
    fig, ax = plt.subplots()
    ax.set_xlim(0, BOARD_SIZE)
    ax.set_ylim(0, BOARD_SIZE)
    ax.set_aspect("equal")
    ax.set_title("PCB Component Placement")

   placements = {
        "USB": (22, 0),  # bottom edge
        "MICROCONTROLLER": (22, 22),  # near center
        "CRYSTAL": (28, 22),  # near microcontroller
        "MIKROBUS1": (0, 15),  # left edge
        "MIKROBUS2": (45, 15),  # right edge
    }
    colors = {
        "USB": "red",
        "MICROCONTROLLER": "blue",
        "CRYSTAL": "orange",
        "MIKROBUS1": "purple",
        "MIKROBUS2": "green",
    }

  for comp, (x, y) in placements.items():
        w, h = COMPONENTS[comp]
        draw_component(ax, comp, x, y, w, h, colors[comp])


  usb_center_x = placements["USB"][0] + COMPONENTS["USB"][0] / 2
    usb_center_y = placements["USB"][1] + COMPONENTS["USB"][1] / 2
    keepout = patches.Rectangle(
        (usb_center_x - 5, placements["USB"][1] + COMPONENTS["USB"][1]), 
        10, 15, linewidth=1, edgecolor="red", facecolor="pink", alpha=0.3, linestyle="--"
    )
    ax.add_patch(keepout)

 plt.show()
if __name__ == "__main__":
    main()
