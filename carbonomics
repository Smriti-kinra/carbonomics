# ===================== CARBONOMICS ===================== #

import os
import mysql.connector
from tabulate import tabulate

# -------------------- CONFIG -------------------- #

DB_PASSWORD = os.getenv("DB_PASSWORD")  # 🔒 set this in your system

# -------------------- DB CONNECTION -------------------- #

mycon = mysql.connector.connect(
    host="localhost",
    user="root",
    password=DB_PASSWORD
)
cur = mycon.cursor()

# -------------------- UI HELPERS -------------------- #

def clear():
    os.system('cls' if os.name == 'nt' else 'clear')

def line():
    print("─" * 70)

def title(text):
    line()
    print(text.center(70))
    line()

def option(num, text):
    print(f"[{num}] {text}")

def success(msg):
    print(f"\n✅ {msg}")

def error(msg):
    print(f"\n❌ {msg}")

def prompt():
    return input("\n👉 Choice: ").strip()

# -------------------- DATABASE SETUP -------------------- #

def setup():
    cur.execute("CREATE DATABASE IF NOT EXISTS CARBONOMICS")
    cur.execute("USE CARBONOMICS")

    cur.execute("""
        CREATE TABLE IF NOT EXISTS STUDY(
            ID INT AUTO_INCREMENT PRIMARY KEY,
            TYPE VARCHAR(20),
            GRP VARCHAR(50),
            FORMULA VARCHAR(100),
            NAME VARCHAR(100)
        )
    """)

    cur.execute("""
        CREATE TABLE IF NOT EXISTS USERS(
            USERNAME VARCHAR(50) PRIMARY KEY,
            PASSWORD VARCHAR(50)
        )
    """)

    cur.execute("""
        CREATE TABLE IF NOT EXISTS SCORE(
            USERNAME VARCHAR(50),
            SCORE INT
        )
    """)

    mycon.commit()

# -------------------- DATA -------------------- #

alkanes = [
    ('CH3-CH(CH3)-CH2-CH3', '2-Methylbutane'),
    ('CH3-C(CH3)2-CH3', '2,2-Dimethylpropane'),
    ('CH3-CH(CH3)-CH(CH3)-CH3', '2,3-Dimethylbutane'),
    ('CH3-CH(CH3)-CH2-CH(CH3)-CH3', '2,4-Dimethylpentane'),
    ('CH3-CH2-CH2-CH(CH2CH3)-CH2-CH3', '3-Ethylhexane')
]

alkenes = [
    ('CH2=C(CH3)-CH2-CH3', '2-Methylbutene'),
    ('CH3-CH=CH-CH2-CH3', 'Pent-2-ene'),
    ('CH3-CH=CH-C(CH3)2-CH3', '4,4-Dimethylpent-2-ene'),
    ('CH3-CH2-CH=CH-CH(CH3)-CH3', '5-Methylhex-3-ene'),
    ('CH2=C(CH3)-CH2-CH(CH2CH3)-CH2-CH2-CH3', '4-Ethyl-2-methylheptene')
]

alkynes = [
    ('CH≡C-CH(CH3)-CH3', '3-Methylbutyne'),
    ('CH3-C≡C-CH(CH3)-CH3', '4-Methylpent-2-yne'),
    ('CH3-C≡C-C(CH3)2-CH2-CH2-CH3', '4,4-Dimethylhept-2-yne'),
    ('CH3-CH(CH3)-C≡C-CH(CH3)-CH3', '2,5-Dimethylhex-3-yne'),
    ('CH3-CH(CH3)-CH2-C≡C-CH2-C(CH3)2-CH3', '2,2,7-Trimethyloct-4-yne')
]

alcohols = [
    ('CH3-CH2-CH2-CH2-OH', 'Butanol'),
    ('CH3-CH(OH)-CH2-CH3', 'Butan-2-ol'),
    ('CH3-CH(OH)-CH2-CH(CH3)-CH3', '4-Methylpentan-2-ol'),
    ('CH3-CH(OH)-CH2-CH(OH)-CH3', 'Pentan-2,4-diol'),
    ('CH3-CH2-CH(OH)-CH(CH2CH3)-CH(CH3)-CH3', '4-Ethyl-5-methylhexan-3-ol')
]

aldehydes = [
    ('CH3-CH2-CHO', 'Propanal'),
    ('CH3-CH(CHO)-CH2-CH3', 'Butan-2-al'),
    ('C6H5-CHO', 'Benzaldehyde'),
    ('CH3-CH(CHO)-CH2-CH(CHO)-CH3', 'Pentan-2,4-dial'),
    ('CH3-CH(CH3)-CH2-CH2-CH2-CHO', '5-Methylhexanal')
]

ketones = [
    ('CH3-CO-CH3', 'Propan-2-one'),
    ('CH3-CH2-CO-CH2-CH3', 'Pentan-3-one'),
    ('CH3-CH(CH2CH3)-CH2-CO-CH3', '4-Ethylbutan-2-one'),
    ('CH3-CH(CH3)-CH2-CO-CH2-CH2-CH2-CH3', '2-Methyloctan-4-one'),
    ('CH3-CO-CH(CH3)-CH2-CH(CH2CH3)-CH3', '5-Ethyl-3-methylhexan-2-one')
]

carboxylic_acids = [
    ('HCOOH', 'Methanoic acid'),
    ('CH3-CH2-COOH', 'Propanoic acid'),
    ('HOOC-CH2-COOH', 'Propanedioic acid'),
    ('HOOC-CH2-CH(COOH)-CH2-COOH', 'Propane-1,2,3-tricarboxylic acid'),
    ('CH3-CH(COOH)-CH2-CH2-CH2-CH3', '2-Methylhexanoic acid')
]

ethers = [
    ('CH3-O-CH3', 'Methoxymethane'),
    ('CH3-O-CH2-CH3', 'Methoxyethane'),
    ('C6H5-O-CH3', 'Methoxybenzene'),
    ('CH3-O-CH(CH3)-CH3', '2-Methoxypropane'),
    ('CH3-O-CH2-CH2-O-CH3', '1,2-Dimethoxyethane')
]

amines = [
    ('CH3-CH2-NH2', 'Ethanamine'),
    ('CH3-CH(NH2)-CH3', 'Propan-2-amine'),
    ('CH3-NH-CH2-CH3', 'N-Methylethanamine'),
    ('CH3-N(CH3)-CH3', 'N,N-Dimethylmethanamine'),
    ('CH3-N(CH3)-CH2-CH2-CH2-CH3', 'N,N-Dimethylbutanamine')
]

alkyl_halides = [
    ('CH3-CH2-CH2-CH2-Br', 'Bromobutane'),
    ('CH3-CH(Cl)-CH3', '2-Chloropropane'),
    ('CH2(Cl)-CH(CH3)-CH2-CH2-CH3', '1-Chloro-2-methylpentane'),
    ('CH3-CH(Cl)-CH2-CH(Br)-CH3', '2-Bromo-4-chloropentane'),
    ('CH3-CH2-CH(I)-CH(CH2CH3)-CH2-CH3', '3-Iodo-4-ethylhexane')
]

poly = [
    ('CH2=CH-CH2-NH2', 'Prop-2-enamine'),
    ('CH3-CH(O-CH3)-CHO', '2-Methoxypropanal'),
    ('CH3-C(CH3)=CH-CO-CH3', '4-Methylpent-3-en-2-one'),
    ('CH3-CH2-CH=CH-OH', 'Butenol'),
    ('CH3-CH2-CH(COOH)-CH2-OH', '2-Ethyl-3-hydroxypropanoic acid')
]

coordination = [
    ('[Ni(CO)4]', 'Tetracarbonylnickel'),
    ('K3[Al(C2O4)3]', 'Potassium trioxalatoaluminate(III)'),
    ('Hg[Co(SCN)4]', 'Mercury(I) tetrathiocyanato-S-cobaltate(III)'),
    ('[Co(Cl)2(en)2]+', 'Dichloridobis(ethane-1,2-diamine)cobalt(III)'),
    ('K2[Zn(OH)4]', 'Potassium tetrahydroxidozincate(II)'),
    ('[Co(NH3)6]Cl3', 'Hexaamminecobalt(III) chloride'),
    ('Fe4[Fe(CN)6]3', 'Iron(III) hexacyanidoferrate(II)'),
    ('[Co(NH3)5Cl]Cl2', 'Pentaamminechloridocobalt(III) chloride'),
    ('K2[Ni(CN)4]', 'Potassium tetracyanidonickelate(II)'),
    ('[Co(NH3)4(H2O)2]Cl3', 'Tetraamminediaquacobalt(III) chloride')
]

# -------------------- INSERT DATA -------------------- #

def insert_data():
    datasets = [
        ("ALKANES", alkanes),
        ("ALKENES", alkenes),
        ("ALKYNES", alkynes),
        ("ALCOHOLS", alcohols),
        ("ALDEHYDES", aldehydes),
        ("KETONES", ketones),
        ("CARBOXYLIC ACIDS", carboxylic_acids),
        ("ETHERS", ethers),
        ("AMINES", amines),
        ("ALKYL HALIDES", alkyl_halides),
        ("POLYFUNCTIONAL", poly)
    ]

    for grp, data in datasets:
        for f, n in data:
            cur.execute(
                "INSERT IGNORE INTO STUDY(TYPE,GRP,FORMULA,NAME) VALUES(%s,%s,%s,%s)",
                ("ORGANIC", grp, f, n)
            )

    for f, n in coordination:
        cur.execute(
            "INSERT IGNORE INTO STUDY(TYPE,FORMULA,NAME) VALUES(%s,%s,%s)",
            ("COORDINATION", f, n)
        )

    mycon.commit()

# -------------------- AUTH -------------------- #

def signup():
    clear()
    title("SIGN UP")

    u = input("Username: ")
    p = input("Password: ")

    cur.execute("SELECT * FROM USERS WHERE USERNAME=%s", (u,))
    if cur.fetchone():
        error("User exists")
        return None

    cur.execute("INSERT INTO USERS VALUES(%s,%s)", (u, p))
    mycon.commit()
    return u

def login():
    clear()
    title("LOGIN")

    u = input("Username: ")
    p = input("Password: ")

    cur.execute("SELECT * FROM USERS WHERE USERNAME=%s AND PASSWORD=%s", (u, p))
    if cur.fetchone():
        return u
    else:
        error("Invalid login")
        return None

# -------------------- STUDY -------------------- #

def study():
    clear()
    title("STUDY")

    cur.execute("SELECT DISTINCT GRP FROM STUDY WHERE GRP IS NOT NULL")
    groups = [g[0] for g in cur.fetchall()]

    for i, g in enumerate(groups, 1):
        option(i, g)

    c = prompt()
    if c.isdigit() and int(c) <= len(groups):
        grp = groups[int(c) - 1]
        cur.execute("SELECT FORMULA,NAME FROM STUDY WHERE GRP=%s", (grp,))
        print(tabulate(cur.fetchall(), headers=["Formula", "Name"], tablefmt="grid"))
        input("\nEnter to continue...")

# -------------------- TEST -------------------- #

def test(user):
    clear()
    title("TEST")

    cur.execute("SELECT FORMULA,NAME FROM STUDY ORDER BY RAND() LIMIT 3")
    qs = cur.fetchall()

    score = 0
    for i, (f, n) in enumerate(qs, 1):
        print(f"\nQ{i}: {f}")
        ans = input("Answer: ")
        if ans.lower() == n.lower():
            score += 1
            success("Correct")
        else:
            error(f"Correct: {n}")

    cur.execute("INSERT INTO SCORE VALUES(%s,%s)", (user, score))
    mycon.commit()

    print(f"\nScore: {score}/3")
    input("Enter to continue...")

# -------------------- ADMIN -------------------- #

def admin():
    clear()
    title("ADMIN")

    option(1, "Add")
    option(2, "Delete")

    c = prompt()

    if c == '1':
        grp = input("Group: ")
        f = input("Formula: ")
        n = input("Name: ")
        cur.execute("INSERT INTO STUDY(TYPE,GRP,FORMULA,NAME) VALUES(%s,%s,%s,%s)",
                    ("ORGANIC", grp, f, n))
        mycon.commit()
        success("Added")

    elif c == '2':
        n = input("Name to delete: ")
        cur.execute("DELETE FROM STUDY WHERE NAME=%s", (n,))
        mycon.commit()
        success("Deleted")

# -------------------- MAIN -------------------- #

def main():
    setup()
    insert_data()

    while True:
        clear()
        title("CARBONOMICS")

        option(1, "Login")
        option(2, "Signup")
        option(3, "Admin")
        option(4, "Exit")

        c = prompt()

        if c == '1':
            user = login()
            if user:
                while True:
                    clear()
                    option(1, "Study")
                    option(2, "Test")
                    option(3, "Logout")

                    ch = prompt()

                    if ch == '1':
                        study()
                    elif ch == '2':
                        test(user)
                    elif ch == '3':
                        break

        elif c == '2':
            user = signup()
            if user:
                success("Logged in")

        elif c == '3':
            admin()

        elif c == '4':
            break

# -------------------- RUN -------------------- #

if __name__ == "__main__":
    main()
