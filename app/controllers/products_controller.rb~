class ProductsController < ApplicationController
  before_action :set_product, only: [:show, :edit, :update, :destroy]

  # GET /products
  # GET /products.json
  def index
    @products = Product.all

    @product_price = []
    @product_name = []
    @product_price_s = []
    @product_rate = []

    @products.each do |product|
      @product_price_s << (product.price).to_i
      @product_price << [(product.price).to_i]
      @product_rate << (product.rate).to_i
      @product_name << product.name
    end
     
    @min_val = @product_price_s.min
    @max_val = @product_price_s.max

    #return render :text => @product_data.inspect
    
    @color=[]      
    @product_name.each do |name|
      @color << "%06x" % (rand * 0xffffff)
    end

    @bar = Gchart.bar(
      :size => '500x300',
      :stacked => false,
      :title => 'Bar chart', 
      :data => @product_price_s,
      :bar_colors => :legend,
      :legend => @product_name,
      :axis_with_labels => ['x','y'],
      :axis_labels => [@product_name, @product_price_s.sort],
      )

    @bar_horizontal = Gchart.bar(
      #:title => 'Horizontal Bar chart',
      :size => '500x300', 
      :stacked => false,  
      :data => @product_price_s,
      :legend => @product_name,
      :bar_colors => :legend,
      :axis_with_labels => ['y','x'],
      :axis_labels => [@product_name, @product_price_s.sort],
      :orientation => 'horizontal'
      )

    @line = Gchart.line(
      :size => '500x300',
      :title => "Line Chart",
      #:axis_with_labels => ['x'],
      :line_colors => :legend,
      :axis_with_labels => ['y','x'],
      :axis_labels => [@product_name, @product_price_s.sort],
      :legend => @product_name,
      :data => @product_price_s.sort
      )
    
    @linexy = Gchart.line(
      :title => "Line XY chart",
      :axis_with_labels => ['y','x'],
      :axis_labels => [@product_rate.sort, @product_price_s.sort],
      :data => [@product_price_s, @product_rate], 
      :line_colors => "FF0000,00FF00"
      )

=begin
    @linexy1 = Gchart.line_xy(
      :size => '200x300',
      :title => "Line XY Chart",
      :axis_with_labels => ['y'],
      :line_colors => @color,
      :xAxis_labels => @product_price, :min_value => 0, :max_value => @max_val,
      :legend => @product_name,
      :data => @product_price_s
      )    
=end
  
    @pie = Gchart.pie(
      :data => @product_price_s,
      :title => 'Pie chart', 
      :size => '400x200', 
      :labels => @product_name,
      :legend => @product_name
      )

    @pie_3d = Gchart.pie_3d(
      :data => @product_price_s,
      :title => 'Pie 3D chart', 
      :size => '400x200',
      :labels => @product_name,
      :legend => @product_name
      )

    @sparkline = Gchart.sparkline( 
  # A sparkline chart has exactly the same parameters as a line chart. The only difference is that the axes lines are not drawn for sparklines by default.
      :title => "Spark Line chart",
      :data => @product_price_s, 
      :size => '100x200', 
      :line_colors => '0077CC'
      )

    @venn = Gchart.venn(
      :title => "Venn chart",
      :data => @product_price_s,
      )
    
    @scatter = Gchart.scatter(
      :title => "Scatter chart",
      :data => @product_price,
      :axis_with_labels => ['x','y'],
      :axis_labels => [@product_name,@product_price_s.sort]
      )
    
    @google_meter = Gchart.meter(
      :title => "Google Meter chart",
      :data => @product_price
      #:label => ['Flavor']
      )

  end

  # GET /products/1
  # GET /products/1.json
  def show
  end

  # GET /products/new
  def new
    @product = Product.new
  end

  # GET /products/1/edit
  def edit
  end

  # POST /products
  # POST /products.json
  def create
    @product = Product.new(product_params)

    respond_to do |format|
      if @product.save
        format.html { redirect_to @product, notice: 'Product was successfully created.' }
        format.json { render :show, status: :created, location: @product }
      else
        format.html { render :new }
        format.json { render json: @product.errors, status: :unprocessable_entity }
      end
    end
  end

  # PATCH/PUT /products/1
  # PATCH/PUT /products/1.json
  def update
    respond_to do |format|
      if @product.update(product_params)
        format.html { redirect_to @product, notice: 'Product was successfully updated.' }
        format.json { render :show, status: :ok, location: @product }
      else
        format.html { render :edit }
        format.json { render json: @product.errors, status: :unprocessable_entity }
      end
    end
  end

  # DELETE /products/1
  # DELETE /products/1.json
  def destroy
    @product.destroy
    respond_to do |format|
      format.html { redirect_to products_url, notice: 'Product was successfully destroyed.' }
      format.json { head :no_content }
    end
  end

  private
    # Use callbacks to share common setup or constraints between actions.
    def set_product
      @product = Product.find(params[:id])
    end

    # Never trust parameters from the scary internet, only allow the white list through.
    def product_params
      params.require(:product).permit(:name, :price, :rate)
    end
end


=begin
line_xy
sparkline
scatter
venn
google meter
line
bar
bar horizontal
pie
pie_3d
=end
