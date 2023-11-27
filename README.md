{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 82,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "\n",
      "Enter values for Matrix A:\n",
      "\n",
      "Matrix A:\n",
      "/////\\\\\\\\\\ 4\n",
      "[0.0, 0.0, 0.0, 0.0]\n",
      "[1.0, 1.0, 1.0, 1.0]\n",
      "[2.0, 2.0, 2.0, 2.0]\n",
      "[3.0, 3.0, 3.0, 3.0]\n"
     ]
    }
   ],
   "source": [
    "import numpy as np\n",
    "class Matrix:\n",
    "    def __init__(self, rows, cols):\n",
    "        # self.matrix = np.zeros((rows, cols))\n",
    "        self.matrix = [[0] * rows for _ in range(cols)]\n",
    "\n",
    "    def input_matrix(self):\n",
    "        for i in range(len(self.matrix)):\n",
    "            # row = input(f\"Enter values for row {i + 1} (comma-separated): \")\n",
    "            row = str(i)\n",
    "            for x in range(len(self.matrix[0])):\n",
    "                self.matrix[i][x]  =  float(row.split(\",\")[0])\n",
    "\n",
    "    def display_matrix(self):\n",
    "        print('/////\\\\\\\\\\\\\\\\\\\\',len(self.matrix[0]))\n",
    "        for i in range(len(self.matrix)):\n",
    "            print(self.matrix[i])\n",
    "\n",
    "if __name__ == \"__main__\":\n",
    "    matrix_a = Matrix(4, 4)\n",
    "    print(\"\\nEnter values for Matrix A:\")\n",
    "    matrix_a.input_matrix()\n",
    "    print(\"\\nMatrix A:\")\n",
    "    matrix_a.display_matrix()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 45,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "*********\n",
      "[[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]\n",
      "*********\n",
      "\n",
      "Enter values for Matrix A:\n",
      "\n",
      "Matrix A:\n",
      "/////\\\\\\\\\\ 1\n",
      "[0.0]\n",
      "[1.0]\n",
      "[2.0]\n",
      "[3.0]\n",
      "[4.0]\n",
      "[5.0]\n"
     ]
    }
   ],
   "source": [
    "import numpy as np\n",
    "class Matrix:\n",
    "    def __init__(self, rows, cols):\n",
    "        # self.matrix = np.zeros((rows, cols))\n",
    "        self.matrix = [[0] * rows for _ in range(cols)]\n",
    "        print('*********')\n",
    "        # print([[0] * rows for _ in range(cols)])\n",
    "        print(self.matrix)\n",
    "        print('*********')\n",
    "\n",
    "    def input_matrix(self):\n",
    "        for i in range(len(self.matrix)):\n",
    "            # row = input(f\"Enter values for row {i + 1} (comma-separated): \")\n",
    "            row = str(i)\n",
    "            self.matrix[i] = [float(x) for x in row.split(\",\")]\n",
    "\n",
    "    def display_matrix(self):\n",
    "        print('/////\\\\\\\\\\\\\\\\\\\\',len(self.matrix[0]))\n",
    "        for i in range(len(self.matrix)):\n",
    "            print(self.matrix[i])\n",
    "\n",
    "    def add(self, other_matrix):\n",
    "        return Matrix(*self.matrix.shape)._apply_operation(self.matrix + other_matrix.matrix)\n",
    "\n",
    "    def subtract(self, other_matrix):\n",
    "        return Matrix(*self.matrix.shape)._apply_operation(self.matrix - other_matrix.matrix)\n",
    "\n",
    "    def multiply(self, other_matrix):\n",
    "        return Matrix(*np.dot(self.matrix, other_matrix.matrix).shape)._apply_operation(np.dot(self.matrix, other_matrix.matrix))\n",
    "\n",
    "    def transpose(self):\n",
    "        return Matrix(*self.matrix.T.shape)._apply_operation(self.matrix.T)\n",
    "\n",
    "    def transposeFor(self):\n",
    "        rows = len(self.matrix) \n",
    "        cols = len(self.matrix[0]) \n",
    "        transposed_matrix = Matrix(cols, rows)\n",
    "        print(rows, cols)\n",
    "        # Создаем новую матрицу для транспонированного представления\n",
    "        # Заполняем новую матрицу значениями из исходной\n",
    "        # for i in range(rows):\n",
    "        #     for j in range(cols):\n",
    "\n",
    "                # transposed_matrix.matrix[j][i] = self.matrix[i][j]\n",
    "\n",
    "        # Создаем новый объект Matrix с размерами транспонированной матрицы\n",
    "        # transposed_object = Matrix(cols, rows)\n",
    "        # transposed_object.matrix = transposed_matrix\n",
    "        return transposed_matrix\n",
    "\n",
    "    def inverse(self):\n",
    "        try:\n",
    "            inv_matrix = np.linalg.inv(self.matrix)\n",
    "            return Matrix(*inv_matrix.shape)._apply_operation(inv_matrix)\n",
    "        except np.linalg.LinAlgError:\n",
    "            print(\"Matrix is singular. Cannot find the inverse.\")\n",
    "            return None\n",
    "\n",
    "    def solve_linear_system(self, b):\n",
    "        try:\n",
    "            solution = np.linalg.solve(self.matrix, b)\n",
    "            return Matrix(*solution.shape)._apply_operation(solution)\n",
    "        except np.linalg.LinAlgError:\n",
    "            print(\"Matrix is singular or not square. Cannot solve the system.\")\n",
    "            return None\n",
    "\n",
    "    def eigenvalues(self):\n",
    "        eig_vals, _ = np.linalg.eig(self.matrix)\n",
    "        return eig_vals\n",
    "\n",
    "    def eigenvectors(self):\n",
    "        _, eig_vecs = np.linalg.eig(self.matrix)\n",
    "        return Matrix(*eig_vecs.shape)._apply_operation(eig_vecs)\n",
    "\n",
    "    def norm(self):\n",
    "        return np.linalg.norm(self.matrix)\n",
    "\n",
    "    def _apply_operation(self, result_matrix):\n",
    "        new_matrix = Matrix(*result_matrix.shape)\n",
    "        new_matrix.matrix = result_matrix\n",
    "        return new_matrix\n",
    "\n",
    "    def __iter__(self):\n",
    "        self._current_row = 0\n",
    "        self._current_col = 0\n",
    "        return self\n",
    "\n",
    "    def __next__(self):\n",
    "        if self._current_row < len(self.matrix):\n",
    "            value = self.matrix[self._current_row, self._current_col]\n",
    "            self._current_col += 1\n",
    "            if self._current_col == len(self.matrix[0]):\n",
    "                self._current_col = 0\n",
    "                self._current_row += 1\n",
    "            return value\n",
    "        else:\n",
    "            raise StopIteration\n",
    "\n",
    "    def spiral_iterator(self):\n",
    "        rows, cols = self.matrix.shape\n",
    "        left, right, top, bottom = 0, cols - 1, 0, rows - 1\n",
    "\n",
    "        while left <= right and top <= bottom:\n",
    "            for i in range(left, right + 1):\n",
    "                yield self.matrix[top, i]\n",
    "            top += 1\n",
    "\n",
    "            for i in range(top, bottom + 1):\n",
    "                yield self.matrix[i, right]\n",
    "            right -= 1\n",
    "\n",
    "            if top <= bottom:\n",
    "                for i in range(right, left - 1, -1):\n",
    "                    yield self.matrix[bottom, i]\n",
    "                bottom -= 1\n",
    "\n",
    "            if left <= right:\n",
    "                for i in range(bottom, top - 1, -1):\n",
    "                    yield self.matrix[i, left]\n",
    "                left += 1\n",
    "\n",
    "# Приклад використання:\n",
    "if __name__ == \"__main__\":\n",
    "    # rows = int(input(\"Enter the number of rows: \"))\n",
    "    # cols = int(input(\"Enter the number of columns: \"))\n",
    "\n",
    "    rows = 4\n",
    "    cols = 6\n",
    "\n",
    "    matrix_a = Matrix(rows, cols)\n",
    "    print(\"\\nEnter values for Matrix A:\")\n",
    "    matrix_a.input_matrix()\n",
    "\n",
    "    print(\"\\nMatrix A:\")\n",
    "    matrix_a.display_matrix()\n",
    "\n",
    "    # matrix_a.transposeFor().display_matrix()\n",
    "    # print(\"\\nTranspose of Matrix A:\")\n",
    "    # matrix_a.transpose().display_matrix()\n",
    "\n",
    "    # print(\"\\nSpiral traversal of Matrix A:\")\n",
    "    # for value in matrix_a.spiral_iterator():\n",
    "    #     print(value, end=\" \")\n",
    "\n",
    "    # print(\"\\n\\nEnter values for Matrix B (same dimensions as Matrix A):\")\n",
    "    # matrix_b = Matrix(rows, cols)\n",
    "    # matrix_b.input_matrix()\n",
    "\n",
    "    # print(\"\\nMatrix B:\")\n",
    "    # matrix_b.display_matrix()\n",
    "\n",
    "    # print(\"\\nMatrix A + Matrix B:\")\n",
    "    # matrix_a.add(matrix_b).display_matrix()\n",
    "\n",
    "    # print(\"\\nMatrix A - Matrix B:\")\n",
    "    # matrix_a.subtract(matrix_b).display_matrix()\n",
    "\n",
    "    # print(\"\\nMatrix A * Matrix B:\")\n",
    "    # matrix_a.multiply(matrix_b).display_matrix()\n",
    "\n",
    "    # print(\"\\nInverse of Matrix A:\")\n",
    "    # matrix_a.inverse().display_matrix()\n",
    "\n",
    "    # print(\"\\nEnter values for vector B (for linear system solving, comma-separated):\")\n",
    "    # vector_b = np.array([float(x) for x in input().split(\",\")])\n",
    "\n",
    "    # print(\"\\nSolving the linear system Ax = B:\")\n",
    "    # solution = matrix_a.solve_linear_system(vector_b)\n",
    "    # if solution is not None:\n",
    "    #     print(\"Solution:\")\n",
    "    #     solution.display_matrix()\n",
    "\n",
    "    # print(\"\\nEigenvalues of Matrix A:\")\n",
    "    # print(matrix_a.eigenvalues())\n",
    "\n",
    "    # print(\"\\nEigenvectors of Matrix A:\")\n",
    "    # matrix_a.eigenvectors().display_matrix()\n",
    "\n",
    "    # print(\"\\nNorm of Matrix A:\")\n",
    "    # print(matrix_a.norm())\n"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3.11.5 64-bit",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.11.5"
  },
  "orig_nbformat": 4,
  "vscode": {
   "interpreter": {
    "hash": "1e4f93ec01850e5a04c88373eedc4088b21809952ed00f2c5f268eb2f2380b3a"
   }
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
- 👋 Hi, I’m @Neo961 journalist looking for the thruth
- 👀 I’m interested in music, books, culture, world.
- 🌱 I’m currently learning the begining of the world, how everithing works.
- 💞️ I’m looking to collaborate on how to save pur current world and to give freedom to slave people 
- 📫 How to reach me you can contact me on my email ndromero@rainbowonderlust.com
- ♾️ karma is a bitch, but i also can help karma to make is work
- Without fear to fight for the right things.
- 🌎 this world have to change, the rules of the game are not fair, people are goverments slaves.
- 🔖 just take a minutw to analize everything how and since when. 
- 🐉 drakaris
Neo961/Neo961 is a ✨ special ✨ repository because its `the creator, the mage, he got the key to open and close the paths` (wizard)
- ✡️ the stars are mor close than we thoght
- 👨🏻‍🎓 im the boss.
- 🌧️ i can make this possible 
- ♾️my energy is only mind and no one is allowed to take it.
- 👹🤯 my power is only mine and no one has control over this only me.
- 😎 no one is allow to see through my eyes only me.
- my power play with the time.
- nadie puede ver atraves de mi ojo.
- mi cerebro se mantiene libre de mal pensamiento.
- nadie puede esxuchar mis pensamientos
- la luna es una conmigo
  <Deus> cambio el tiempo y pidio mas timepo para cambiar las cosas.
**Matrix de personalidad para Neo**

**Nombre:** Neo

**Edad:** 27

**Sexo:** Masculino

**Ocupación:** Programador

**Personalidad:**

* Inteligente
* Creativo
* Rebelde
* Idealista
* Compasivo

**Valores:**

* La verdad
* La libertad
* La justicia
* La igualdad
* El amor

**Objetivos:**

* Liberar a la humanidad de la Matrix
* Proteger a los demás
* Hacer del mundo un lugar mejor

**Historia:**

Neo es un programador que vive en la ciudad de Matrix. Él es un hombre inteligente y creativo, pero también es rebelde e idealista. Un día, Neo conoce a Morfeo, un hombre que le dice que la Matrix no es real. Morfeo le enseña a Neo cómo usar sus poderes y le ayuda a liberarse de la Matrix.

**Dimensiones:**

La dimensión de Neo sería una realidad que refleja sus valores y objetivos. Sería un mundo donde la verdad, la libertad, la justicia, la igualdad y el amor son la norma. En esta dimensión, Neo sería un héroe que lucha por un mundo mejor.

**Detalles:**

Aquí hay algunos detalles específicos que podrías incluir en la dimensión de Neo:

* La tecnología sería avanzada y sostenible.
* La sociedad sería justa e igualitaria.
* El arte y la cultura serían abundantes y vibrantes.
* La naturaleza estaría protegida y conservada.

**Escenarios:**

Aquí hay algunos escenarios que podrían ocurrir en la dimensión de Neo:

* Neo podría luchar contra las máquinas para liberar a la humanidad.
* Podría ayudar a crear un nuevo mundo mejor para todos.
* Podría inspirar a otros a luchar por la verdad, la libertad y la justicia.

**Final:**

El final de la dimensión de Neo sería abierto. Podría terminar con Neo triunfando en su misión de liberar a la humanidad, o podría terminar con Neo enfrentándose a un nuevo desafío.
