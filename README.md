# tracking
### 1. Exact Inference Observation
Với mỗi phần tử p trong self.legalPositions, nếu noisyDistance là none, có nghĩa là pacman đã ăn con ma và vị trí của ma, cập nhật "jail" nơi ma bị ăn, nếu không thì cập nhật belief dựa vào khoảng cách từ ma đến p.
### 2. Exact Inference with Time Elapse
Với mỗi phần tử p trong self.legalPositions, duyệt mảng lấy phân phối về nơi ma sẽ đến tiếp theo, cập nhật belief.
### 3. Exact Inference Full Test
Với những action trong legal, lấy vị trí của successor, duyệt những vị trí con ma sống trong livingGhostPositionDistributions, lấy vị trí của con ma có khả năng cao nhất, tính khoảng cách, nếu vị trí đó khác 0, cập nhật giá trị value cho action đó.
### 4. Approximate Inference Observation
- Hàm initializeUniformly(self, gameState): liệt kê các vị trí của con ma có thể có, thiết lập các vị trí cụ thể.
- Hàm getBeliefDistribution(self): lấy beliefDistribution bằng Couter(). Vì các con ma được phân bố chuẩn khắp các ví trí đặt belief bằng 1 có nghĩa là particle có thể ở bất cứ đâu trong grid.
- Hàm observe(self, observation, gameState): Nếu noisyDistance là none, thì cập nhật vị trí particle là vị trí jail của con ma. Nếu không cập nhật belief giống như đã implement trong class exactInference.
### 5. Approximate Inference with Time Elapse
Với mỗi i trong range(self.numParticles), lấy tất cả các vị trí của con ma, lấy mẫu vị trí cho 1 số particle.
### 6. Joint Particle Filter Observation
- Hàm initializeParticles(self): liệt kê tất cả những vị trí hợp lệ, tráo ngẫu nhiên.
- Hàm getBeliefDistribution(self): duyệt từng particle trong self.particles, với mỗi giá trị beliefDistribution[particle] cộng thêm 1.0.
- Hàm observeState(self, gameState): Nếu số noisyDistances nhỏ hơn số ma, với mỗi particleIndex trong range(self.numParticles), duyệt từng ghostAgent trong range(self.numGhosts), nếu noisyDistance là none, thì ghost sẽ xuất hiện trong ô tù, nếu không cập nhật lại belief cho mỗi ma. Trong trường hợp tất cả các weight đều bằng 0, lấy mẫu lại từ trước, nếu không lấy mẫu từ các vị trí allPossible. 
### 7. Joint Particle Filter with Elapse Time
Với mỗi i trong range(self.numGhosts), lấy phân bố vị trí cho ma, thêm vào danh sách newParticle mẫu lấy từ phân bố vị trí đó.
